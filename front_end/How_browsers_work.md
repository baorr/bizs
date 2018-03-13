<div class="toc">  
<ol>
<li><a href="#Introduction">Introduction</a>
<ol>
    <li><a href="#The_browsers_we_will_talk_about">The browsers we will talk about</a></li>
    <li><a href="#The_browser_main_functionality">The browser's main functionality</a></li>
    <li><a href="#The_browser_high_level_structure">The browser's high level structure</a></li>
    <li><a href="#Communication_between_the_components">Communication_between the components</a></li>
</ol>
</li>
<li><a href="#The_rendering_engine">The rendering engine</a>
<ol>
    <li><a href="#Rendering_engines">Rendering engines</a></li>
    <li><a href="#The_main_flow">The main flow</a></li>
    <li><a href="#Main_flow_examples">Main flow examples</a></li>
    <li><a href="#Parsing_general">Parsing and DOM tree construction</a>
    <ol>
        <li><a href="#Parsing_general">Parsing - general</a>
        <ol>
            <li><a href="#Grammars">Grammars</a></li>
            <li><a href="#Parser_Lexer_combination">Parser - Lexer combination</a></li>
            <li><a href="#Translation">Translation</a></li>
            <li><a href="#Parsing_example">Parsing example</a></li>
            <li><a href="#Formal_definitions_for_vocabulary_and_syntax">Formal definitions for vocabulary and syntax</a></li>
            <li><a href="#Types_of_parsers">Types of parsers</a></li>
            <li><a href="#Generating_parsers_automatically">Generating parsers automatically</a></li>
        </ol>
        </li>
        <li><a href="#HTML_Parser">HTML Parser</a>
        <ol>
          <li><a href="#The_HTML_grammar_definition">The HTML grammar definition</a></li>
          <li><a href="#Not_a_context_free_grammar">Not a context free grammar</a></li>
          <li><a href="#HTML_DTD">HTML DTD</a></li>
          <li><a href="#DOM">DOM</a></li>
          <li><a href="#The_parsing_algorithm">The parsing algorithm</a></li>
          <li><a href="#The_tokenization_algorithm">The tokenization algorithm</a></li>
          <li><a href="#Tree_construction_algorithm">Tree construction algorithm</a></li>
          <li><a href="#Actions_when_the_parsing_is_finished">Actions when the parsing is finished</a></li>
          <li><a href="#Browsers_error_tolerance">Browsers error tolerance</a></li>
        </ol>
        </li>
        <li><a href="#CSS_parsing">CSS parsing</a>
        <ol>
          <li><a href="#Webkit_CSS_parser">Webkit CSS parser</a></li>
        </ol>
        </li>
        <li><a href="#Parsing_scripts">Parsing scripts</a></li>
        <li><a href="#The_order_of_processing_scripts_and_style_sheets">The order of processing scripts and style sheets</a>
        <ol>
          <li><a href="#Scripts">Scripts</a></li>
          <li><a href="#Speculative_parsing">Speculative parsing</a></li>
          <li><a href="#Style_sheets">Style sheets</a></li>
        </ol>
        </li>
    </ol>
    </li>
    <li><a href="#Render_tree_construction">Render tree construction</a>
    <ol>
      <li><a href="#The_render_tree_relation_to_the_DOM_tree">The render tree relation to the DOM tree</a></li>
      <li><a href="#The_flow_of_constructing_the_tree">The flow of constructing the tree</a></li>
      <li><a href="#Style_Computation">Style Computation</a>
      <ol>
        <li><a href="#Sharing_style_data">Sharing style data</a></li>
        <li><a href="#Firefox_rule_tree">Firefox rule tree</a>
        <ol>
            <li><a href="#Division_into_structs">Division into structs</a></li>
          <li><a href="#Computing_the_style_contexts_using_the_rule_tree">Computing the style contexts using the rule       tree</a></li>
        </ol>
        </li>
        <li><a href="#Manipulating_the_rules_for_an_easy_match">Manipulating the rules for an easy match</a></li>
        <li><a href="#Applying_the_rules_in_the_correct_cascade_order">Applying the rules in the correct cascade order</a>
        <ol>
        <li><a href="#Style_sheet_cascade_order">Style sheet cascade order</a></li>
        <li><a href="#Specifity">Specifity</a></li>
        <li><a href="#Sorting_the_rules">Sorting the rules</a></li>
        </ol>
        </li>
      </ol>
      </li>
      <li><a href="#Gradual_process">Gradual process</a></li>
    </ol>
    </li>
     <li><a href="#Layout">Layout</a>
      <ol>
        <li><a href="#Dirty_bit_system">Dirty bit system</a></li>
        <li><a href="#Global_and_incremental_layout">Global and incremental layout</a></li>
        <li><a href="#Asynchronous_and_Synchronous_layout">Asynchronous and Synchronous layout</a></li>
        <li><a href="#Optimizations">Optimizations</a></li>
        <li><a href="#The_layout_process">The layout process</a></li>
        <li><a href="#Width_calculation">Width calculation</a></li>
        <li><a href="#Line_Breaking">Line Breaking</a></li>
      </ol>
     </li>
     <li><a href="#Painting">Painting</a>
      <ol>
        <li><a href="#Global_and_Incremental">Global and Incremental</a></li>
        <li><a href="#The_painting_order">The painting order</a></li>
        <li><a href="#Firefox_display_list">Firefox display list</a></li>
        <li><a href="#Webkit_rectangle_storage">Webkit rectangle storage</a></li>
      </ol>
     </li>
     <li><a href="#Dynamic_changes">Dynamic changes</a></li>
     <li><a href="#The_rendering_engines_threads">The rendering engine's threads</a>
      <ol>
        <li><a href="#Event_loop">Event loop</a></li>
      </ol> 
     </li>
      <li><a href="#css">CSS2 visual model</a>
      <ol>
        <li><a href="#The_canvas">The canvas</a></li>
        <li><a href="#CSS_Box_model">CSS Box model</a></li>
        <li><a href="#Positioning_scheme">Positioning scheme</a></li>
        <li><a href="#Box_types">Box types</a></li>
        <li><a href="#Positioning">Positioning</a>
        <ol>
            <li><a href="#Relative">Relative</a></li>
            <li><a href="#Floats">Floats</a></li>
            <li><a href="#Absolute_and_fixed">Absolute and fixed</a></li>
        </ol>
        </li>
        <li><a href="#Layered_representation">Layered representation</a></li>
      </ol>
     </li>
     <li><a href="#Resources">Resources</a></li>
</ol>   
</li>
</ol>
</div>
