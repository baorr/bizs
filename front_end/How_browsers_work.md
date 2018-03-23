# 浏览器工作原理
### 主流浏览器背后的工作场景
<div class="toc">  
<ol>
<li><a href="#Introduction">简介</a>
<ol>
    <li><a href="#The_browsers_we_will_talk_about">我们涉及到的浏览器</a></li>
    <li><a href="#The_browser_main_functionality">浏览器主要的功能</a></li>
    <li><a href="#The_browser_high_level_structure">浏览器的顶层架构</a></li>
    <li><a href="#Communication_between_the_components">各组件之间的通信</a></li>
</ol>
</li>
<li><a href="#The_rendering_engine">渲染引擎</a>
<ol>
    <li><a href="#Rendering_engines">各种浏览器的渲染引擎</a></li>
    <li><a href="#The_main_flow">渲染的主流程</a></li>
    <li><a href="#Main_flow_examples">渲染的主流程举例</a></li>
    <li><a href="#Parsing_general">解析和DOM树的构建</a>
    <ol>
        <li><a href="#Parsing_general">解析-通用</a>
        <ol>
            <li><a href="#Grammars">语法</a></li>
            <li><a href="#Parser_Lexer_combination">解析 - 词法分析程序的组合</a></li>
            <li><a href="#Translation">转码</a></li>
            <li><a href="#Parsing_example">转码示例</a></li>
            <li><a href="#Formal_definitions_for_vocabulary_and_syntax">词汇和语法的定义</a></li>
            <li><a href="#Types_of_parsers">编译器的种类</a></li>
            <li><a href="#Generating_parsers_automatically">自动产生编译器</a></li>
        </ol>
        </li>
        <li><a href="#HTML_Parser">编译HTML</a>
        <ol>
          <li><a href="#The_HTML_grammar_definition">HTML 语法定义</a></li>
          <li><a href="#Not_a_context_free_grammar">Not a context free grammar</a></li>
          <li><a href="#HTML_DTD">HTML DTD</a></li>
          <li><a href="#DOM">DOM</a></li>
          <li><a href="#The_parsing_algorithm">编译算法</a></li>
          <li><a href="#The_tokenization_algorithm">The tokenization 算法</a></li>
          <li><a href="#Tree_construction_algorithm">构建树算法</a></li>
          <li><a href="#Actions_when_the_parsing_is_finished">Actions when the parsing is finished</a></li>
          <li><a href="#Browsers_error_tolerance">浏览器容错处理</a></li>
        </ol>
        </li>
        <li><a href="#CSS_parsing">编译CSS</a>
        <ol>
          <li><a href="#Webkit_CSS_parser">Webkit内核的CSS解析器</a></li>
        </ol>
        </li>
        <li><a href="#Parsing_scripts">编译脚本</a></li>
        <li><a href="#The_order_of_processing_scripts_and_style_sheets">处理CSS和脚本的顺序</a>
        <ol>
          <li><a href="#Scripts">脚本</a></li>
          <li><a href="#Speculative_parsing">推测编译</a></li>
          <li><a href="#Style_sheets">样式表</a></li>
        </ol>
        </li>
    </ol>
    </li>
    <li><a href="#Render_tree_construction">渲染构建树</a>
    <ol>
      <li><a href="#The_render_tree_relation_to_the_DOM_tree">渲染树和DOM树的关系</a></li>
      <li><a href="#The_flow_of_constructing_the_tree">构造树的流程</a></li>
      <li><a href="#Style_Computation">样式计算</a>
      <ol>
        <li><a href="#Sharing_style_data">共享样式数据</a></li>
        <li><a href="#Firefox_rule_tree">Firefox规则树</a>
        <ol>
            <li><a href="#Division_into_structs">Division into structs</a></li>
          <li><a href="#Computing_the_style_contexts_using_the_rule_tree">Computing the style contexts using the rule  tree</a></li>
        </ol>
        </li>
        <li><a href="#Manipulating_the_rules_for_an_easy_match">Manipulating the rules for an easy match</a></li>
        <li><a href="#Applying_the_rules_in_the_correct_cascade_order">Applying the rules in the correct cascade order</a>
        <ol>
        <li><a href="#Style_sheet_cascade_order">级联样式的顺序</a></li>
        <li><a href="#Specifity">特例</a></li>
        <li><a href="#Sorting_the_rules">规则排序</a></li>
        </ol>
        </li>
      </ol>
      </li>
      <li><a href="#Gradual_process">平滑处理</a></li>
    </ol>
    </li>
     <li><a href="#Layout">定位</a>
      <ol>
        <li><a href="#Dirty_bit_system">Dirty bit system</a></li>
        <li><a href="#Global_and_incremental_layout">Global and incremental layout</a></li>
        <li><a href="#Asynchronous_and_Synchronous_layout">同步和异步定位</a></li>
        <li><a href="#Optimizations">定位优化</a></li>
        <li><a href="#The_layout_process">The layout process</a></li>
        <li><a href="#Width_calculation">Width calculation</a></li>
        <li><a href="#Line_Breaking">Line Breaking</a></li>
      </ol>
     </li>
     <li><a href="#Painting">绘制</a>
      <ol>
        <li><a href="#Global_and_Incremental">Global and Incremental</a></li>
        <li><a href="#The_painting_order">绘制顺序</a></li>
        <li><a href="#Firefox_display_list">Firefox display list</a></li>
        <li><a href="#Webkit_rectangle_storage">Webkit rectangle storage</a></li>
      </ol>
     </li>
     <li><a href="#Dynamic_changes">动态改变</a></li>
     <li><a href="#The_rendering_engines_threads">渲染引擎的线程</a>
      <ol>
        <li><a href="#Event_loop">事件循环</a></li>
      </ol> 
     </li>
      <li><a href="#css">CSS2可视化模型</a>
      <ol>
        <li><a href="#The_canvas">画布</a></li>
        <li><a href="#CSS_Box_model">CSS盒子模型</a></li>
        <li><a href="#Positioning_scheme">定位方式</a></li>
        <li><a href="#Box_types">盒子模型类型</a></li>
        <li><a href="#Positioning">定位</a>
        <ol>
            <li><a href="#Relative">相对定位</a></li>
            <li><a href="#Floats">浮动定位</a></li>
            <li><a href="#Absolute_and_fixed">绝对和固定定位</a></li>
        </ol>
        </li>
        <li><a href="#Layered_representation">层次展示</a></li>
      </ol>
     </li>
     <li><a href="#Resources">相关资料</a></li>
</ol>   
</li>
</ol>
</div>
