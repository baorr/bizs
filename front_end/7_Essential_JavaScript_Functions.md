<article itemscope="" itemtype="http://schema.org/Article"><h1 itemprop="headline" class="offscreen">7必须知道JS函数</h1><div class="meta" id="meta">
By
<a href="http://davidwalsh.name" itemprop="author" itemscope="" itemtype="https://schema.org/Person"><span itemprop="name">David Walsh</span></a>&nbsp;on
<time itemprop="datePublished">June 2, 2015</time>
&nbsp;
</div><div class="offscreen"></div><!-- content --><p>I remember the early days of JavaScript where you needed a simple function for just about everything because the browser vendors implemented&nbsp;features differently, and not just&nbsp;edge features, basic features, like <code>addEventListener</code> and <code>attachEvent</code>. &nbsp;Times have changed but there are still a few functions each developer should have in their arsenal, for performance for functional ease purposes.</p><div class="x x-long x-secondary"><a href="https://tkjs.us/2qjWxOs" style="display:block;"><object data="https://davidwalsh.name/demo/track-js-2.svg?1522306226" type="image/svg+xml" style="max-width:100%;pointer-events:none;"></object></a></div>

<h2><a href="https://davidwalsh.name/javascript-debounce-function"><code>debounce</code></a></h2>

<p>The debounce function can be a game-changer when it comes to&nbsp;event-fueled performance. &nbsp;If you aren't using a debouncing function with a <code>scroll</code>, <code>resize</code>, <code>key*</code> event, you're probably doing it&nbsp;wrong. &nbsp;Here's a <code>debounce</code> function to keep your code&nbsp;efficient:</p>

<pre class=" language-js" prism="1"><span class="token comment" spellcheck="true">// Returns a function, that, as long as it continues to be invoked, will not</span>
<span class="token comment" spellcheck="true">// be triggered. The function will be called after it stops being called for</span>
<span class="token comment" spellcheck="true">// N milliseconds. If `immediate` is passed, trigger the function on the</span>
<span class="token comment" spellcheck="true">// leading edge, instead of the trailing.</span>
<span class="token keyword">function</span> <span class="token function">debounce</span><span class="token punctuation">(</span>func<span class="token punctuation">,</span> wait<span class="token punctuation">,</span> immediate<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">var</span> timeout<span class="token punctuation">;</span>
    <span class="token keyword">return</span> <span class="token keyword">function</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">var</span> context <span class="token operator">=</span> <span class="token keyword">this</span><span class="token punctuation">,</span> args <span class="token operator">=</span> arguments<span class="token punctuation">;</span>
        <span class="token keyword">var</span> later <span class="token operator">=</span> <span class="token keyword">function</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            timeout <span class="token operator">=</span> <span class="token keyword">null</span><span class="token punctuation">;</span>
            <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span>immediate<span class="token punctuation">)</span> func<span class="token punctuation">.</span><span class="token function">apply</span><span class="token punctuation">(</span>context<span class="token punctuation">,</span> args<span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span><span class="token punctuation">;</span>
        <span class="token keyword">var</span> callNow <span class="token operator">=</span> immediate <span class="token operator">&amp;&amp;</span> <span class="token operator">!</span>timeout<span class="token punctuation">;</span>
        <span class="token function">clearTimeout</span><span class="token punctuation">(</span>timeout<span class="token punctuation">)</span><span class="token punctuation">;</span>
        timeout <span class="token operator">=</span> <span class="token function">setTimeout</span><span class="token punctuation">(</span>later<span class="token punctuation">,</span> wait<span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">if</span> <span class="token punctuation">(</span>callNow<span class="token punctuation">)</span> func<span class="token punctuation">.</span><span class="token function">apply</span><span class="token punctuation">(</span>context<span class="token punctuation">,</span> args<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">;</span>

<span class="token comment" spellcheck="true">// Usage</span>
<span class="token keyword">var</span> myEfficientFn <span class="token operator">=</span> <span class="token function">debounce</span><span class="token punctuation">(</span><span class="token keyword">function</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token comment" spellcheck="true">// All the taxing stuff you do</span>
<span class="token punctuation">}</span><span class="token punctuation">,</span> <span class="token number">250</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
window<span class="token punctuation">.</span><span class="token function">addEventListener</span><span class="token punctuation">(</span><span class="token string">'resize'</span><span class="token punctuation">,</span> myEfficientFn<span class="token punctuation">)</span><span class="token punctuation">;</span></pre>

<p>The <code>debounce</code> function will&nbsp;not allow a callback to be used more than once per given time frame. &nbsp;This is especially important&nbsp;when assigning&nbsp;a callback function to frequently-firing events.</p>

<h2><a href="https://davidwalsh.name/javascript-polling"><code>poll</code></a></h2>

<p>As I mentioned with the <code>debounce</code> function, sometimes you don't get to plug into an event to&nbsp;signify a desired state --&nbsp;if the event doesn't exist, you need to check for your desired&nbsp;state at intervals:</p>

<pre class=" language-js" prism="1"><span class="token comment" spellcheck="true">// The polling function</span>
<span class="token keyword">function</span> <span class="token function">poll</span><span class="token punctuation">(</span>fn<span class="token punctuation">,</span> timeout<span class="token punctuation">,</span> interval<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">var</span> endTime <span class="token operator">=</span> <span class="token function">Number</span><span class="token punctuation">(</span><span class="token keyword">new</span> <span class="token class-name">Date</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token operator">+</span> <span class="token punctuation">(</span>timeout <span class="token operator">||</span> <span class="token number">2000</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    interval <span class="token operator">=</span> interval <span class="token operator">||</span> <span class="token number">100</span><span class="token punctuation">;</span>

    <span class="token keyword">var</span> checkCondition <span class="token operator">=</span> <span class="token keyword">function</span><span class="token punctuation">(</span>resolve<span class="token punctuation">,</span> reject<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment" spellcheck="true">// If the condition is met, we're done! </span>
        <span class="token keyword">var</span> result <span class="token operator">=</span> <span class="token function">fn</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">if</span><span class="token punctuation">(</span>result<span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token function">resolve</span><span class="token punctuation">(</span>result<span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        <span class="token comment" spellcheck="true">// If the condition isn't met but the timeout hasn't elapsed, go again</span>
        <span class="token keyword">else</span> <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token function">Number</span><span class="token punctuation">(</span><span class="token keyword">new</span> <span class="token class-name">Date</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token operator">&lt;</span> endTime<span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token function">setTimeout</span><span class="token punctuation">(</span>checkCondition<span class="token punctuation">,</span> interval<span class="token punctuation">,</span> resolve<span class="token punctuation">,</span> reject<span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        <span class="token comment" spellcheck="true">// Didn't match and too much time, reject!</span>
        <span class="token keyword">else</span> <span class="token punctuation">{</span>
            <span class="token function">reject</span><span class="token punctuation">(</span><span class="token keyword">new</span> <span class="token class-name">Error</span><span class="token punctuation">(</span><span class="token string">'timed out for '</span> <span class="token operator">+</span> fn <span class="token operator">+</span> <span class="token string">': '</span> <span class="token operator">+</span> arguments<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span><span class="token punctuation">;</span>

    <span class="token keyword">return</span> <span class="token keyword">new</span> <span class="token class-name">Promise</span><span class="token punctuation">(</span>checkCondition<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token comment" spellcheck="true">// Usage:  ensure element is visible</span>
<span class="token function">poll</span><span class="token punctuation">(</span><span class="token keyword">function</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">return</span> document<span class="token punctuation">.</span><span class="token function">getElementById</span><span class="token punctuation">(</span><span class="token string">'lightbox'</span><span class="token punctuation">)</span><span class="token punctuation">.</span>offsetWidth <span class="token operator">&gt;</span> <span class="token number">0</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">,</span> <span class="token number">2000</span><span class="token punctuation">,</span> <span class="token number">150</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">then</span><span class="token punctuation">(</span><span class="token keyword">function</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token comment" spellcheck="true">// Polling done, now do something else!</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token keyword">catch</span><span class="token punctuation">(</span><span class="token keyword">function</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token comment" spellcheck="true">// Polling timed out, handle the error!</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span></pre>

<p>Polling has long been useful on the web and will continue to be in the future!</p>

<h2><a href="https://davidwalsh.name/javascript-once"><code>once</code></a></h2>

<p>There are times when you prefer a given functionality only happen once, similar to the way you'd use an <code>onload</code> event. &nbsp;This code&nbsp;provides you said functionality:</p>

<pre class=" language-js" prism="1"><span class="token keyword">function</span> <span class="token function">once</span><span class="token punctuation">(</span>fn<span class="token punctuation">,</span> context<span class="token punctuation">)</span> <span class="token punctuation">{</span> 
    <span class="token keyword">var</span> result<span class="token punctuation">;</span>

    <span class="token keyword">return</span> <span class="token keyword">function</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span> 
        <span class="token keyword">if</span><span class="token punctuation">(</span>fn<span class="token punctuation">)</span> <span class="token punctuation">{</span>
            result <span class="token operator">=</span> fn<span class="token punctuation">.</span><span class="token function">apply</span><span class="token punctuation">(</span>context <span class="token operator">||</span> <span class="token keyword">this</span><span class="token punctuation">,</span> arguments<span class="token punctuation">)</span><span class="token punctuation">;</span>
            fn <span class="token operator">=</span> <span class="token keyword">null</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>

        <span class="token keyword">return</span> result<span class="token punctuation">;</span>
    <span class="token punctuation">}</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token comment" spellcheck="true">// Usage</span>
<span class="token keyword">var</span> canOnlyFireOnce <span class="token operator">=</span> <span class="token function">once</span><span class="token punctuation">(</span><span class="token keyword">function</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span><span class="token string">'Fired!'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token function">canOnlyFireOnce</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment" spellcheck="true">// "Fired!"</span>
<span class="token function">canOnlyFireOnce</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment" spellcheck="true">// nada</span></pre>

<p>The <code>once</code> function ensures a given function can only be called once, thus prevent duplicate initialization!</p>

<h2><a href="https://davidwalsh.name/get-absolute-url"><code>getAbsoluteUrl</code></a></h2>

<p>Getting an absolute URL from a variable string isn't as easy as you think. &nbsp;There's the&nbsp;<code>URL</code> constructor but it can act up if you don't provide the required arguments (which sometimes you can't). &nbsp;Here's a suave trick for getting an absolute URL from and string input:</p>

<pre class=" language-js" prism="1"><span class="token keyword">var</span> getAbsoluteUrl <span class="token operator">=</span> <span class="token punctuation">(</span><span class="token keyword">function</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">var</span> a<span class="token punctuation">;</span>

    <span class="token keyword">return</span> <span class="token keyword">function</span><span class="token punctuation">(</span>url<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">if</span><span class="token punctuation">(</span><span class="token operator">!</span>a<span class="token punctuation">)</span> a <span class="token operator">=</span> document<span class="token punctuation">.</span><span class="token function">createElement</span><span class="token punctuation">(</span><span class="token string">'a'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        a<span class="token punctuation">.</span>href <span class="token operator">=</span> url<span class="token punctuation">;</span>

        <span class="token keyword">return</span> a<span class="token punctuation">.</span>href<span class="token punctuation">;</span>
    <span class="token punctuation">}</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment" spellcheck="true">// Usage</span>
<span class="token function">getAbsoluteUrl</span><span class="token punctuation">(</span><span class="token string">'/something'</span><span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment" spellcheck="true">// https://davidwalsh.name/something</span></pre>

<p>The "burn" element <code>href</code>&nbsp;handles and URL nonsense for you, providing a reliable&nbsp;absolute URL in return.</p>

<h2><a href="https://davidwalsh.name/detect-native-function"><code>isNative</code></a></h2>

<p>Knowing if a given function&nbsp;is native or not can signal if you're willing&nbsp;to override it. &nbsp;This handy code can give you the answer:</p>

<pre class=" language-js" prism="1"><span class="token punctuation">;</span><span class="token punctuation">(</span><span class="token keyword">function</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>

  <span class="token comment" spellcheck="true">// Used to resolve the internal `[[Class]]` of values</span>
  <span class="token keyword">var</span> toString <span class="token operator">=</span> Object<span class="token punctuation">.</span>prototype<span class="token punctuation">.</span>toString<span class="token punctuation">;</span>
  
  <span class="token comment" spellcheck="true">// Used to resolve the decompiled source of functions</span>
  <span class="token keyword">var</span> fnToString <span class="token operator">=</span> Function<span class="token punctuation">.</span>prototype<span class="token punctuation">.</span>toString<span class="token punctuation">;</span>
  
  <span class="token comment" spellcheck="true">// Used to detect host constructors (Safari &gt; 4; really typed array specific)</span>
  <span class="token keyword">var</span> reHostCtor <span class="token operator">=</span> <span class="token regex">/^\[object .+?Constructor\]$/</span><span class="token punctuation">;</span>

  <span class="token comment" spellcheck="true">// Compile a regexp using a common native method as a template.</span>
  <span class="token comment" spellcheck="true">// We chose `Object#toString` because there's a good chance it is not being mucked with.</span>
  <span class="token keyword">var</span> reNative <span class="token operator">=</span> <span class="token function">RegExp</span><span class="token punctuation">(</span><span class="token string">'^'</span> <span class="token operator">+</span>
    <span class="token comment" spellcheck="true">// Coerce `Object#toString` to a string</span>
    <span class="token function">String</span><span class="token punctuation">(</span>toString<span class="token punctuation">)</span>
    <span class="token comment" spellcheck="true">// Escape any special regexp characters</span>
    <span class="token punctuation">.</span><span class="token function">replace</span><span class="token punctuation">(</span><span class="token regex">/[.*+?^${}()|[\]\/\\]/g</span><span class="token punctuation">,</span> <span class="token string">'\\$&amp;'</span><span class="token punctuation">)</span>
    <span class="token comment" spellcheck="true">// Replace mentions of `toString` with `.*?` to keep the template generic.</span>
    <span class="token comment" spellcheck="true">// Replace thing like `for ...` to support environments like Rhino which add extra info</span>
    <span class="token comment" spellcheck="true">// such as method arity.</span>
    <span class="token punctuation">.</span><span class="token function">replace</span><span class="token punctuation">(</span><span class="token regex">/toString|(function).*?(?=\\\()| for .+?(?=\\\])/g</span><span class="token punctuation">,</span> <span class="token string">'$1.*?'</span><span class="token punctuation">)</span> <span class="token operator">+</span> <span class="token string">'$'</span>
  <span class="token punctuation">)</span><span class="token punctuation">;</span>
  
  <span class="token keyword">function</span> <span class="token function">isNative</span><span class="token punctuation">(</span>value<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">var</span> type <span class="token operator">=</span> <span class="token keyword">typeof</span> value<span class="token punctuation">;</span>
    <span class="token keyword">return</span> type <span class="token operator">==</span> <span class="token string">'function'</span>
      <span class="token comment" spellcheck="true">// Use `Function#toString` to bypass the value's own `toString` method</span>
      <span class="token comment" spellcheck="true">// and avoid being faked out.</span>
      <span class="token operator">?</span> reNative<span class="token punctuation">.</span><span class="token function">test</span><span class="token punctuation">(</span>fnToString<span class="token punctuation">.</span><span class="token function">call</span><span class="token punctuation">(</span>value<span class="token punctuation">)</span><span class="token punctuation">)</span>
      <span class="token comment" spellcheck="true">// Fallback to a host object check because some environments will represent</span>
      <span class="token comment" spellcheck="true">// things like typed arrays as DOM methods which may not conform to the</span>
      <span class="token comment" spellcheck="true">// normal native pattern.</span>
      <span class="token punctuation">:</span> <span class="token punctuation">(</span>value <span class="token operator">&amp;&amp;</span> type <span class="token operator">==</span> <span class="token string">'object'</span> <span class="token operator">&amp;&amp;</span> reHostCtor<span class="token punctuation">.</span><span class="token function">test</span><span class="token punctuation">(</span>toString<span class="token punctuation">.</span><span class="token function">call</span><span class="token punctuation">(</span>value<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token operator">||</span> <span class="token boolean">false</span><span class="token punctuation">;</span>
  <span class="token punctuation">}</span>
  
  <span class="token comment" spellcheck="true">// export however you want</span>
  module<span class="token punctuation">.</span>exports <span class="token operator">=</span> isNative<span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment" spellcheck="true">// Usage</span>
<span class="token function">isNative</span><span class="token punctuation">(</span>alert<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment" spellcheck="true">// true</span>
<span class="token function">isNative</span><span class="token punctuation">(</span>myCustomFunction<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment" spellcheck="true">// false</span></pre>

<p>The function isn't pretty but it gets the job done!</p>

<h2><a href="https://davidwalsh.name/add-rules-stylesheets"><code>insertRule</code></a></h2>

<p>We all know that we can grab a NodeList&nbsp;from a selector (via <code>document.querySelectorAll</code>) and give each of them a style, but what's more efficient is setting that style to a selector (like you do in a stylesheet):</p>

<pre class=" language-js" prism="1"><span class="token keyword">var</span> sheet <span class="token operator">=</span> <span class="token punctuation">(</span><span class="token keyword">function</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token comment" spellcheck="true">// Create the &lt;style&gt; tag</span>
    <span class="token keyword">var</span> style <span class="token operator">=</span> document<span class="token punctuation">.</span><span class="token function">createElement</span><span class="token punctuation">(</span><span class="token string">'style'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

    <span class="token comment" spellcheck="true">// Add a media (and/or media query) here if you'd like!</span>
    <span class="token comment" spellcheck="true">// style.setAttribute('media', 'screen')</span>
    <span class="token comment" spellcheck="true">// style.setAttribute('media', 'only screen and (max-width : 1024px)')</span>

    <span class="token comment" spellcheck="true">// WebKit hack :(</span>
    style<span class="token punctuation">.</span><span class="token function">appendChild</span><span class="token punctuation">(</span>document<span class="token punctuation">.</span><span class="token function">createTextNode</span><span class="token punctuation">(</span><span class="token string">''</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

    <span class="token comment" spellcheck="true">// Add the &lt;style&gt; element to the page</span>
    document<span class="token punctuation">.</span>head<span class="token punctuation">.</span><span class="token function">appendChild</span><span class="token punctuation">(</span>style<span class="token punctuation">)</span><span class="token punctuation">;</span>

    <span class="token keyword">return</span> style<span class="token punctuation">.</span>sheet<span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment" spellcheck="true">// Usage</span>
sheet<span class="token punctuation">.</span><span class="token function">insertRule</span><span class="token punctuation">(</span><span class="token string">"header { float: left; opacity: 0.8; }"</span><span class="token punctuation">,</span> <span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">;</span></pre>

<p>This is especially&nbsp;useful when working on a dynamic, AJAX-heavy site. &nbsp;If you set the style to a selector, you don't need to account for styling each element that may match that selector (now or in the future).</p>

<h2><a href="https://davidwalsh.name/element-matches-selector"><code>matchesSelector</code></a></h2>

<p>Oftentimes we validate input before moving forward; ensuring a truthy value, ensuring forms&nbsp;data is valid, etc. &nbsp;But how often do we ensure an element qualifies for moving forward? &nbsp;You can use a <code>matchesSelector</code> function to validate if an element is of a given selector match:</p>

<pre class=" language-js" prism="1"><span class="token keyword">function</span> <span class="token function">matchesSelector</span><span class="token punctuation">(</span>el<span class="token punctuation">,</span> selector<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">var</span> p <span class="token operator">=</span> Element<span class="token punctuation">.</span>prototype<span class="token punctuation">;</span>
    <span class="token keyword">var</span> f <span class="token operator">=</span> p<span class="token punctuation">.</span>matches <span class="token operator">||</span> p<span class="token punctuation">.</span>webkitMatchesSelector <span class="token operator">||</span> p<span class="token punctuation">.</span>mozMatchesSelector <span class="token operator">||</span> p<span class="token punctuation">.</span>msMatchesSelector <span class="token operator">||</span> <span class="token keyword">function</span><span class="token punctuation">(</span>s<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">return</span> <span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">.</span>indexOf<span class="token punctuation">.</span><span class="token function">call</span><span class="token punctuation">(</span>document<span class="token punctuation">.</span><span class="token function">querySelectorAll</span><span class="token punctuation">(</span>s<span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token keyword">this</span><span class="token punctuation">)</span> <span class="token operator">!==</span> <span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span><span class="token punctuation">;</span>
    <span class="token keyword">return</span> f<span class="token punctuation">.</span><span class="token function">call</span><span class="token punctuation">(</span>el<span class="token punctuation">,</span> selector<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token comment" spellcheck="true">// Usage</span>
<span class="token function">matchesSelector</span><span class="token punctuation">(</span>document<span class="token punctuation">.</span><span class="token function">getElementById</span><span class="token punctuation">(</span><span class="token string">'myDiv'</span><span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token string">'div.someSelector[some-attribute=true]'</span><span class="token punctuation">)</span></pre>

<p>There you have it: &nbsp;seven JavaScript functions that every developer should keep in their toolbox. &nbsp;Have a function I missed? &nbsp;Please share it!</p><!-- secondary ad -->
<!-- guest blogger --></article>