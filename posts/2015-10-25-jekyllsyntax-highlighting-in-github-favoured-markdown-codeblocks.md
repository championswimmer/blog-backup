---
title: "Jekyll:Syntax Highlighting in Github Favoured Markdown codeblocks"
slug: jekyllsyntax-highlighting-in-github-favoured-markdown-codeblocks
date_published: 2015-10-25T00:00:00.000Z
date_updated: 2015-10-25T00:00:00.000Z
---

base01    #586e75  body text / default code / primary content

base1     #93a1a1  comments / secondary content

base3     #fdf6e3  background

orange    #cb4b16  constants

red       #dc322f  regex, special keywords

blue      #268bd2  reserved keywords

cyan      #2aa198  strings, numbers

green     #859900  operators, other keywords

*/

.highlight { background-color: #fdf6e3; color: #586e75; max-width: 56.25rem; padding: 1rem; border-radius: 1rem; margin: 0px auto 2em; }

.highlight .lineno { color: #93a1a1 } /* Line Numbers */

.highlight .c { color: #93a1a1 } /* Comment */

.highlight .err { color: #586e75 } /* Error */

.highlight .g { color: #586e75 } /* Generic */

.highlight .k { color: #859900 } /* Keyword */

.highlight .l { color: #586e75 } /* Literal */

.highlight .n { color: #586e75 } /* Name */

.highlight .o { color: #859900 } /* Operator */

.highlight .x { color: #cb4b16 } /* Other */

.highlight .p { color: #586e75 } /* Punctuation */

.highlight .cm { color: #93a1a1 } /* Comment.Multiline */

.highlight .cp { color: #859900 } /* Comment.Preproc */

.highlight .c1 { color: #93a1a1 } /* Comment.Single */

.highlight .cs { color: #859900 } /* Comment.Special */

.highlight .gd { color: #2aa198 } /* Generic.Deleted */

.highlight .ge { color: #586e75; font-style: italic } /* Generic.Emph */

.highlight .gr { color: #dc322f } /* Generic.Error */

.highlight .gh { color: #cb4b16 } /* Generic.Heading */

.highlight .gi { color: #859900 } /* Generic.Inserted */

.highlight .go { color: #586e75 } /* Generic.Output */

.highlight .gp { color: #586e75 } /* Generic.Prompt */

.highlight .gs { color: #586e75; font-weight: bold } /* Generic.Strong */

.highlight .gu { color: #cb4b16 } /* Generic.Subheading */

.highlight .gt { color: #586e75 } /* Generic.Traceback */

.highlight .kc { color: #cb4b16 } /* Keyword.Constant */

.highlight .kd { color: #268bd2 } /* Keyword.Declaration */

.highlight .kn { color: #859900 } /* Keyword.Namespace */

.highlight .kp { color: #859900 } /* Keyword.Pseudo */

.highlight .kr { color: #268bd2 } /* Keyword.Reserved */

.highlight .kt { color: #dc322f } /* Keyword.Type */

.highlight .ld { color: #586e75 } /* Literal.Date */

.highlight .m { color: #2aa198 } /* Literal.Number */

.highlight .s { color: #2aa198 } /* Literal.String */

.highlight .na { color: #586e75 } /* Name.Attribute */

.highlight .nb { color: #B58900 } /* Name.Builtin */

.highlight .nc { color: #268bd2 } /* Name.Class */

.highlight .no { color: #cb4b16 } /* Name.Constant */

.highlight .nd { color: #268bd2 } /* Name.Decorator */

.highlight .ni { color: #cb4b16 } /* Name.Entity */

.highlight .ne { color: #cb4b16 } /* Name.Exception */

.highlight .nf { color: #268bd2 } /* Name.Function */

.highlight .nl { color: #586e75 } /* Name.Label */

.highlight .nn { color: #586e75 } /* Name.Namespace */

.highlight .nx { color: #586e75 } /* Name.Other */

.highlight .py { color: #586e75 } /* Name.Property */

.highlight .nt { color: #268bd2 } /* Name.Tag */

.highlight .nv { color: #268bd2 } /* Name.Variable */

.highlight .ow { color: #859900 } /* Operator.Word */

.highlight .w { color: #586e75 } /* Text.Whitespace */

.highlight .mf { color: #2aa198 } /* Literal.Number.Float */

.highlight .mh { color: #2aa198 } /* Literal.Number.Hex */

.highlight .mi { color: #2aa198 } /* Literal.Number.Integer */

.highlight .mo { color: #2aa198 } /* Literal.Number.Oct */

.highlight .sb { color: #93a1a1 } /* Literal.String.Backtick */

.highlight .sc { color: #2aa198 } /* Literal.String.Char */

.highlight .sd { color: #586e75 } /* Literal.String.Doc */

.highlight .s2 { color: #2aa198 } /* Literal.String.Double */

.highlight .se { color: #cb4b16 } /* Literal.String.Escape */

.highlight .sh { color: #586e75 } /* Literal.String.Heredoc */

.highlight .si { color: #2aa198 } /* Literal.String.Interpol */

.highlight .sx { color: #2aa198 } /* Literal.String.Other */

.highlight .sr { color: #dc322f } /* Literal.String.Regex */

.highlight .s1 { color: #2aa198 } /* Literal.String.Single */

.highlight .ss { color: #2aa198 } /* Literal.String.Symbol */

.highlight .bp { color: #268bd2 } /* Name.Builtin.Pseudo */

.highlight .vc { color: #268bd2 } /* Name.Variable.Class */

.highlight .vg { color: #268bd2 } /* Name.Variable.Global */

.highlight .vi { color: #268bd2 } /* Name.Variable.Instance */

.highlight .il { color: #2aa198 } /* Literal.Number.Integer.Long */

    
    Make sure to add `<link rel="stylesheet" href="{{ site.url }}/assets/css/pygments/solarized-light.css">` to the layout of your posts. Most probably might be in _includes/head.html or specifically in _layouts/post.html
    
    That should be it. Your Jekyll blog posts, with GFM code blocks should now be highlighted in Solarized, if all went well. 
    As a proof, I am using the same method in this very block. Feel free to check out the sources. 
