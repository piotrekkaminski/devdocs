---
layout: default
group:
subgroup: Testing
title: JavaScript unit tests
menu_title: JavaScript unit tests
menu_order: 2
github_link: extension-dev-guide/test/test_js-unit.md
redirect_from: /guides/v1.0/extension-dev-guide/test/test_js-unit.html
---

<p>Magento JavaScript unit tests use the external <a href="#test-library">JsTestDriver test library</a>. The tests are implemented through the external <a href="#jstestdriver-api">JsTestDriver API</a> and have their own <a href="#framework">jsunit.requirejsUtil framework</a>.</p>
<p>After you run the PHP interpreter once to run unit tests, you can <a href="#phpstorm">run the JavaScript unit tests from the PhpStorm IDE</a>.</p>
<p>To run JavaScript unit tests, read these topics:</p>
<ul>
<li><a href="#unit-test-overview">Overview</a></li>
<li><a href="#config-files">Configuration files</a></li>
<li><a href="#process-overview">run_js_tests.php script</a></li>
<li><a href="#test-prereqs">Step 1. Before you begin</a></li>
<li><a href="#main-api">Step 2. Configure unit tests</a></li>
<li><a href="#run-js-unit-tests">Step 3. Run unit tests</a></li>
<li><a href="#phpstorm">Step 4. Use PhpStorm to run unit tests</a></li>
</ul>
<h2 id="unit-test-overview">Overview</h2>
<p>To run the automated JavaScript unit tests, you run the <a href="#process-overview">run_js_tests.php script</a> inside the PHP interpreter from the command line. When you run the PHP script, it reads <a href="#config-files">configuration files</a> in the <code>/dev/tests/js</code> directory. It also generates a <code>jsTestDriver.conf</code> YAML configuration file in the <code>/dev/tests/js</code> directory. The JsTestDriver reads this generated file to run the tests. After the PHP interpreter runs for the first time, you can run the unit tests from the <a href="#phpstorm">PhpStorm IDE</a>.</p>
<h3 id="test-library">JsTestDriver test library</h3>

<p>Magento JavaScript unit tests use the external <a href="https://code.google.com/p/js-test-driver/wiki/GettingStarted">JsTestDriver</a> library, which follows JUnit principles. The PHPUnit library also follows these principles.</p>
<h3 id="jstestdriver-api">JsTestDriver API</h3>
<p>The unit tests are implemented through the JsTestDriver API. Web developers should be familiar with this API and test structure.</p>
<h3 id="framework">jsunit.requirejsUtil framework</h3>
<p>The unit tests also have their own framework. The <code>framework/requirejs-util.js</code> file declares the <code>jsunit.requirejsUtil</code> framework object, which supports testing of <code>RequireJS</code> (AMD) modules.</p>
<p>These modules actively call the global <code>define()</code> function immediately upon loading rather than passively declaring their classes or functions. <code>RequireJS</code> modules usually do not expose anything to the global state. Instead, the modules pass all declarations to the <code>define()</code> function.</p>
<p>This organization enables testing of <code>RequireJS</code> modules without any additional Magento test framework (MTF) support. <code>jsunit.requirejsUtil</code> intercepts all <code>define()</code> calls and can pass <code>RequireJS</code> modules to their corresponding tests.</p>
<p>For example:</p>
<p><b>dev/tests/js/testsuite/mage/requirejs/plugin/id-normalizer-test.js:</b></p>

<pre>
var IdNormalizerTest = TestCase('IdNormalizerTest');

IdNormalizerTest.prototype.setUp = function() {
    var defineArgs = jsunit.requirejsUtil.getDefineArgsInScript('lib/web/mage/requirejs/plugin/id-normalizer.js');

    assertNotUndefined('There expected to be a define() call', defineArgs);
    assertEquals('Wrong number of arguments in the define() call', 1, defineArgs.length);

    this.normalizer = defineArgs[0]; // Now we have object to be tested
};
</pre>

<h2 id="config-files">Configuration files</h2>
<p>The <code>run_js_tests.php</code> script processes the <a href="#jstestdrivephp">jsTestDriver.php.dist</a> and <a href="#jstestdriverorderphp">jsTestDriverOrder.php</a> configuration files.
   Both files reside in the <code>/dev/tests/js</code> directory.
</p>
<h3 id="jstestdrivephp">jsTestDriver.php.dist file</h3>
<p>This file specifies the contents of the YAML configuration file used by JsTestDriver.
   This file contains this PHP code:
</p>
<p><b>dev/tests/js/jsTestDriver.php.dist:</b></p>

   <pre>
&lt;?php
return array(
    'server' => 'http://localhost:9876',
    'proxy' => array(array('matcher' => '/lib/web/*', 'server' => '%s/test/%s/lib/web/')),
    'load' => array(
        '/lib/web/globalize',
        '/lib/web/jquery/ui',
        '/lib/web/mage/localization',
        '/lib/web/mage/validation',
        '/lib/web/mage/components'),
    'test' => array('/dev/tests/js/testsuite'),
    'serve' => array('/lib/web/mage/calendar')
);
</pre>

<p>For a description of these configuration parameters, see <a href="https://code.google.com/p/js-test-driver/wiki/ConfigurationFile">Configuration file for test runner</a>.</p>
<p>These parameters are:</p>
<ul>
   <li>
      <b>server</b>. The default location of the JsTestDriver server in the form: <code>http://&lt;hostname>:&lt;port></code>
   </li>
   <li>
      <b>proxy</b>. Sets the JsTestDriver to behave as a proxy. The proxy parameter is an array of arrays that enables you to specify multiple matcher and server proxies.
   </li>
   <li>
      <b>load</b>. Defines the list of files to load in the browser before any tests run.
   </li>
   <li>
      <b>test</b>. Defines the list of test sources to run.
   </li>
   <li>
      <b>serve</b>. Defines the list of static files to load by using the same domain as the JsTestDriver.
   </li>
</ul>
<h3 id="jstestdriverorderphp">jsTestDriverOrder.php file</h3>
<p>
   This file specifies the order in which the JsTestDriver loads certain JavaScript files. This file contains this PHP code:
</p>
<p><b>dev/tests/js/jsTestDriverOrder.php:</b></p>

   <pre>
&lt;?php
return array(
    '/lib/web/globalize/globalize.js',
    '/lib/web/jquery/jquery.js',
    '/lib/web/jquery/ui/jquery-ui.js',
    ...
);
</pre>

<p>The array applies load ordering to the files specified by the <b>load</b> parameter in the <code>jsTestDriver.php</code> or <code>jsTestDriver.php.dist</code> file.</p>
<h2 id="process-overview">run_js_tests.php script</h2>
<p>To run the automated unit tests, you run the <a href="#process-overview">run_js_tests.php script</a> inside the PHP interpreter from the command line.</p>
<p>To complete the unit tests, the PHP script completes this processing:</p>
<ol>

   <li>
      <p>The script looks for the <b>JsTestDriver</b> parameter value in a <code>jsTestDriver</code> configuration file in the <code>/dev/tests/js</code> directory.</p>
      <p>If found, the script uses the custom <code>jsTestDriver.php</code> configuration file.</p>
      <p>Otherwise, the script uses the default <code>jsTestDriver.php.dist</code> configuration file.</p>
   </li>
   <li>
      <p>The script looks for the <b>Browser</b> parameter value in the <code>jsTestDriver</code> configuration file that it found.</p>
      <p>If the parameter is not set in the configuration file, the script uses to the default browser location, as follows:</p>
      <ul>
         <li>
            <p><b>64-bit Windows</b>. The location is <code>C:\Program Files (x86)\Mozilla Firefox\firefox.exe</code>.</p>
         </li>
         <li>
            <p><b>Linux</b>. The script runs the <code>which firefox</code> command to determine the location of the Firefox executable in your PATH.</p>
         </li>
      </ul>
   </li>
   <li>
      <p>If the script finds the browser executable and the <code>JsTestDriver.jar</code> file, it proceeds with the next step. Otherwise, the script fails.</p>
   </li>
   <li>
      <p>The script determines the order in which the JsTestDriver loads certain JavaScript files through the <code>jsTestDriverOrder.php</code> configuration file in the <code>/dev/tests/js</code> directory.</p>
   </li>
</ol>
<h2 id="test-prereqs">Step 1. Before you begin</h2>
<p>On the system where you plan to run the unit tests, install the following prerequisite software:</p>
<ul>
   <li><b>PHP</b></p></li>
   <li>
      <p><b>The Firefox browser</b></p>
      <p>On 64-bit Windows machines, the default installation directory is <code>C:\Program Files (x86)\Mozilla Firefox\firefox.exe</code>.</p>
      <p>On Linux machines, locate the browser executable in your PATH.</p>
   </li>
   <li>
      <p><b>The <code>JsTestDriver.jar</code> file</b></p>
   </li>
</ul>
<h2 id="main-api">Step 2. Configure unit tests</h2>
<p>Configuration files are located in the <code>/dev/tests/js</code> directory.</p>
<p>In a custom <code>jsTestDriver.php</code> configuration file or the default <code>jsTestDriver.php.dist</code> file, set these configuration parameters:</p>
<dl>
   <dt>Browser</dt>
   <dd>
      <p>Defines the file path to the executable for the browser.</p>
      <p>If you do not set this value, the script uses to the default browser location, as follows:</p>
      <ul>
         <li>
            <p><b>64-bit Windows</b>. The location is <code>C:\Program Files (x86)\Mozilla Firefox\firefox.exe</code>.</p>
         </li>
         <li>
            <p><b>Linux</b>. The script runs the <code>which firefox</code> command to determine the location of the Firefox executable in your PATH.</p>
         </li>
      </ul>
   </dd>
   <dt>JsTestDriver</dt>
   <dd>
      <p>Required. Defines the file path to the <code>JsTestDriver.jar</code> file.</p>
   </dd>
</dl>
<h2 id="run-js-unit-tests">Step 3. Run unit tests</h2>
<p>To run the automated JavaScript tests, run the <code>run_js_tests.php</code> script inside the PHP interpreter from the command line:</p>

   <pre>
c:\git\magento2\dev\tests\js>php run_js_tests.php
</pre>

<p>Find the test results in individual <code>.xml</code> files in the <code>dev/tests/js/test-output</code> directory.</p>
<p>The output of the PHP command resembles this output:</p>
<p><b>JsTestDriver output:</b></p>

   <pre>
c:\git\magento2\dev\tests\js>php run_js_tests.php
java -jar C:\Users\mchiocca\lib\JsTestDriver.jar --config C:\git\magento2\dev\tests\js/jsTestDriver.conf --port 9876 --browser "C:\Program Files (x86)\Mozilla Firefox\firefox.exe" --tests all --testOutput C:\git\magento2\dev\tests\js/test-output
setting runnermode QUIET
....................................
Total 36 tests (Passed: 36; Fails: 0; Errors: 0) (138.00 ms)
  Firefox 15.0 Windows: Run 36 tests (Passed: 36; Fails: 0; Errors 0) (138.00 ms)
  </pre>

<p>On Linux, the X Server might generate one or more warning messages in the output:</p>
<p><b>X Server warning messages on Linux:</b></p>

<pre>
FreeFontPath: FPE "unix/:7100" refcount is 2, should be 1; fixing.
</pre>

<p>An X Server bug causes these benign messages, which you can ignore.</p>
<p>When you run the PHP script, it reads two configuration files. It also generates a <code>jsTestDriver.conf</code> YAML configuration file in the <code>/dev/tests/js</code> directory. The JsTestDriver reads this generated file to run the tests.</p>
<p>The contents of jsTestDriver.conf resembles this:</p>
<p><b>Generated jsTestDriver.conf file:</b></p>

<pre>
server: http://localhost:9876
proxy:
  - {matcher: "/lib/web/*", server: "http://localhost:9876/test/C:/git/magento2/lib/web/"}
  ...
load:
  - ../../../lib/web/globalize/globalize.js
  ...
test:
  - ../../../dev/tests/js/testsuite/mage/calendar/calendar-test.js
  ...
serve:
  - ../../../lib/web/mage/calendar/calendar.js
  ...
</pre>

<h2 id="phpstorm">Step 4. Use PhpStorm to run unit tests</h2>
<p>After the PHP interpreter runs for the first time, you can <a href="#phpstorm">run the JavaScript unit tests from the PhpStorm IDE</a>.</p>
<p>Complete these steps to use PhpStorm to run unit tests:</p>
<ol>
<li><a href="#install-plugin">Install the JsTestDriver plugin</a></li>
<li><a href="#start-jstestdriver-server">Start the JsTestDriver server</a></li>
<li><a href="#run-configuration">Create a run configuration</a></li>
<li><a href="#capture-browser">Capture a browser</a></li>
</ol>
<h3 id="install-plugin">Install the JsTestDriver plugin</h3>
<ol>
   <li>In PhpStorm, open <b>Settings</b> and select <b>Plugins</b>.</li>
   <li>Click <b>Browse Repositories...</b>.</li>
   <li>Right-click <b>JSTestDriver Plugin</b> and select <b>Download and Install</b>.</li>
   <li>Restart PhpStorm.</li>
</ol>
<h3 id="start-jstestdriver-server">Start the JsTestDriver server</h3>
<ol>
   <li>At the bottom of the IDE, click <b>JsTestDriver Server</b>.</li>
   <li>
      <p>In the <b>JsTestDriver Server</b> panel, click the green right arrow to start the server.</p>
      <p>The bar changes to yellow and reads <code>There are no captured browsers</code>.</p>
   </li>
</ol>
<h3 id="run-configuration">Create a run configuration</h3>
<ol>
<li>Enter a name for the run configuration.</li>
<li>Select <b>Configuration File</b> and provide the location of the <code>jsTestDriver.conf</code> file generated by PHP.</li>
<li>Select <b>Running in IDE</b>.</li>
<li>
   <p>Click <b>Test Connection</b>.</p>
   <p>The <code>Connection to http://localhost:9876 is OK, no captured browsers</code> message appears.</p>
</li>
</ol>
<h3 id="capture-browser">Capture a browser</h3>
<ol>
   <li>
      <p>In the <b>JsTestDriver Server</b> panel, click a browser icon.</p>
      <p>The selected browser opens. In the browser, a green header shows the <code>Server: Waiting...</code> message.</p>
      <p>The colored bar in the <b>JsTestDriver Server</b> panel turns green.</p>
      <p>The <code>Ready to run tests</code> message appears.</p>
   </li>
   <li>
      <p>To run the unit tests, select <b>Run Configuration</b> and click the <b>Run</b> icon.</p>
      <p>A panel at the bottom of the IDE shows the test results.</p>
   </li>
   <li>
      <p>Depending on whether you have changed one or more configuration files, complete the appropriate step to run the tests:</p>
<ul>
         <li>
            <p><b>No changed configuration files</b></p>
            <p>Use PhpStorm to run the tests.</p>
            <p>Before you can run the tests, click the red square icon in the <b>JsTestDriver Server</b> panel to stop the JsTestDriver server that runs in PhpStorm. You must also close the captured browser.</p>
         </li>
         <li>
            <p><b>One or more changed configuration files</b></p>
            <p>Use the PHP interpreter at the command line to regenerate the <code>jsTestDriver.conf</code> file and run the tests.</p>
         </li>
      </ul>
   </li>
</ol>