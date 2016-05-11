---
layout: post
title: "Travelling Salesman Problem"
date: 2016-05-10 17:20:20 +0700
categories: data_mining python
tags: data_mining scraping python
---

<html>
<head><meta charset="utf-8" />
<title>travelling_salesman_problem</title>

<script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.0.3/jquery.min.js"></script>

<style type="text/css">
    /*!
*
* Twitter Bootstrap
*
*//*! normalize.css v3.0.2 | MIT License | git.io/normalize */html{font-family:sans-serif;-ms-text-size-adjust:100%;-webkit-text-size-adjust:100%;font-size:10px;-webkit-tap-highlight-color:transparent}article,aside,details,figcaption,figure,footer,header,hgroup,main,menu,nav,section,summary{display:block}audio,canvas,progress,video{display:inline-block;vertical-align:baseline}audio:not([controls]){display:none;height:0}[hidden],template{display:none}a{background-color:transparent}a:active,a:hover{outline:0}abbr[title]{border-bottom:1px dotted}b,optgroup,strong{font-weight:700}dfn{font-style:italic}h1{font-size:2em;margin:.67em 0}mark{background:#ff0;color:#000}small{font-size:80%}sub,sup{font-size:75%;line-height:0;position:relative;vertical-align:baseline}sup{top:-.5em}sub{bottom:-.25em}img{border:0;vertical-align:middle}svg:not(:root){overflow:hidden}hr{-moz-box-sizing:content-box;box-sizing:content-box;height:0}pre,textarea{overflow:auto}code,kbd,pre,samp{font-size:1em}button,input,optgroup,select,textarea{color:inherit;font:inherit;margin:0}button{overflow:visible}button,select{text-transform:none}button,html input[type=button],input[type=reset],input[type=submit]{-webkit-appearance:button;cursor:pointer}button[disabled],html input[disabled]{cursor:default}button::-moz-focus-inner,input::-moz-focus-inner{border:0;padding:0}input{line-height:normal}input[type=checkbox],input[type=radio]{box-sizing:border-box;padding:0}input[type=number]::-webkit-inner-spin-button,input[type=number]::-webkit-outer-spin-button{height:auto}input[type=search]::-webkit-search-cancel-button,input[type=search]::-webkit-search-decoration{-webkit-appearance:none}table{border-collapse:collapse;border-spacing:0}td,th{padding:0}/*! Source: https://github.com/h5bp/html5-boilerplate/blob/master/src/css/main.css */@media print{*,:after,:before{background:0 0!important;color:#000!important;box-shadow:none!important;text-shadow:none!important}a,a:visited{text-decoration:underline}a[href]:after{content:" (" attr(href)")"}abbr[title]:after{content:" (" attr(title)")"}a[href^="javascript:"]:after,a[href^="#"]:after{content:""}blockquote,pre{border:1px solid #999;page-break-inside:avoid}thead{display:table-header-group}img,tr{page-break-inside:avoid}img{max-width:100%!important}h2,h3,p{orphans:3;widows:3}h2,h3{page-break-after:avoid}select{background:#fff!important}.navbar{display:none}.btn>.caret,.dropup>.btn>.caret{border-top-color:#000!important}.label{border:1px solid #000}.table{border-collapse:collapse!important}.table td,.table th{background-color:#fff!important}.table-bordered td,.table-bordered th{border:1px solid #ddd!important}}@font-face{font-family:'Glyphicons Halflings';src:url(../components/bootstrap/fonts/glyphicons-halflings-regular.eot);src:url(../components/bootstrap/fonts/glyphicons-halflings-regular.eot?#iefix)format('embedded-opentype'),url(../components/bootstrap/fonts/glyphicons-halflings-regular.woff2)format('woff2'),url(../components/bootstrap/fonts/glyphicons-halflings-regular.woff)format('woff'),url(../components/bootstrap/fonts/glyphicons-halflings-regular.ttf)format('truetype'),url(../components/bootstrap/fonts/glyphicons-halflings-regular.svg#glyphicons_halflingsregular)format('svg')}.glyphicon{position:relative;top:1px;display:inline-block;font-family:'Glyphicons Halflings';font-style:normal;font-weight:400;line-height:1;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale}.glyphicon-asterisk:before{content:"\2a"}.glyphicon-plus:before{content:"\2b"}.glyphicon-eur:before,.glyphicon-euro:before{content:"\20ac"}.glyphicon-minus:before{content:"\2212"}.glyphicon-cloud:before{content:"\2601"}.glyphicon-envelope:before{content:"\2709"}.glyphicon-pencil:before{content:"\270f"}.glyphicon-glass:before{content:"\e001"}.glyphicon-music:before{content:"\e002"}.glyphicon-search:before{content:"\e003"}.glyphicon-heart:before{content:"\e005"}.glyphicon-star:before{content:"\e006"}.glyphicon-star-empty:before{content:"\e007"}.glyphicon-user:before{content:"\e008"}.glyphicon-film:before{content:"\e009"}.glyphicon-th-large:before{content:"\e010"}.glyphicon-th:before{content:"\e011"}.glyphicon-th-list:before{content:"\e012"}.glyphicon-ok:before{content:"\e013"}.glyphicon-remove:before{content:"\e014"}.glyphicon-zoom-in:before{content:"\e015"}.glyphicon-zoom-out:before{content:"\e016"}.glyphicon-off:before{content:"\e017"}.glyphicon-signal:before{content:"\e018"}.glyphicon-cog:before{content:"\e019"}.glyphicon-trash:before{content:"\e020"}.glyphicon-home:before{content:"\e021"}.glyphicon-file:before{content:"\e022"}.glyphicon-time:before{content:"\e023"}.glyphicon-road:before{content:"\e024"}.glyphicon-download-alt:before{content:"\e025"}.glyphicon-download:before{content:"\e026"}.glyphicon-upload:before{content:"\e027"}.glyphicon-inbox:before{content:"\e028"}.glyphicon-play-circle:before{content:"\e029"}.glyphicon-repeat:before{content:"\e030"}.glyphicon-refresh:before{content:"\e031"}.glyphicon-list-alt:before{content:"\e032"}.glyphicon-lock:before{content:"\e033"}.glyphicon-flag:before{content:"\e034"}.glyphicon-headphones:before{content:"\e035"}.glyphicon-volume-off:before{content:"\e036"}.glyphicon-volume-down:before{content:"\e037"}.glyphicon-volume-up:before{content:"\e038"}.glyphicon-qrcode:before{content:"\e039"}.glyphicon-barcode:before{content:"\e040"}.glyphicon-tag:before{content:"\e041"}.glyphicon-tags:before{content:"\e042"}.glyphicon-book:before{content:"\e043"}.glyphicon-bookmark:before{content:"\e044"}.glyphicon-print:before{content:"\e045"}.glyphicon-camera:before{content:"\e046"}.glyphicon-font:before{content:"\e047"}.glyphicon-bold:before{content:"\e048"}.glyphicon-italic:before{content:"\e049"}.glyphicon-text-height:before{content:"\e050"}.glyphicon-text-width:before{content:"\e051"}.glyphicon-align-left:before{content:"\e052"}.glyphicon-align-center:before{content:"\e053"}.glyphicon-align-right:before{content:"\e054"}.glyphicon-align-justify:before{content:"\e055"}.glyphicon-list:before{content:"\e056"}.glyphicon-indent-left:before{content:"\e057"}.glyphicon-indent-right:before{content:"\e058"}.glyphicon-facetime-video:before{content:"\e059"}.glyphicon-picture:before{content:"\e060"}.glyphicon-map-marker:before{content:"\e062"}.glyphicon-adjust:before{content:"\e063"}.glyphicon-tint:before{content:"\e064"}.glyphicon-edit:before{content:"\e065"}.glyphicon-share:before{content:"\e066"}.glyphicon-check:before{content:"\e067"}.glyphicon-move:before{content:"\e068"}.glyphicon-step-backward:before{content:"\e069"}.glyphicon-fast-backward:before{content:"\e070"}.glyphicon-backward:before{content:"\e071"}.glyphicon-play:before{content:"\e072"}.glyphicon-pause:before{content:"\e073"}.glyphicon-stop:before{content:"\e074"}.glyphicon-forward:before{content:"\e075"}.glyphicon-fast-forward:before{content:"\e076"}.glyphicon-step-forward:before{content:"\e077"}.glyphicon-eject:before{content:"\e078"}.glyphicon-chevron-left:before{content:"\e079"}.glyphicon-chevron-right:before{content:"\e080"}.glyphicon-plus-sign:before{content:"\e081"}.glyphicon-minus-sign:before{content:"\e082"}.glyphicon-remove-sign:before{content:"\e083"}.glyphicon-ok-sign:before{content:"\e084"}.glyphicon-question-sign:before{content:"\e085"}.glyphicon-info-sign:before{content:"\e086"}.glyphicon-screenshot:before{content:"\e087"}.glyphicon-remove-circle:before{content:"\e088"}.glyphicon-ok-circle:before{content:"\e089"}.glyphicon-ban-circle:before{content:"\e090"}.glyphicon-arrow-left:before{content:"\e091"}.glyphicon-arrow-right:before{content:"\e092"}.glyphicon-arrow-up:before{content:"\e093"}.glyphicon-arrow-down:before{content:"\e094"}.glyphicon-share-alt:before{content:"\e095"}.glyphicon-resize-full:before{content:"\e096"}.glyphicon-resize-small:before{content:"\e097"}.glyphicon-exclamation-sign:before{content:"\e101"}.glyphicon-gift:before{content:"\e102"}.glyphicon-leaf:before{content:"\e103"}.glyphicon-fire:before{content:"\e104"}.glyphicon-eye-open:before{content:"\e105"}.glyphicon-eye-close:before{content:"\e106"}.glyphicon-warning-sign:before{content:"\e107"}.glyphicon-plane:before{content:"\e108"}.glyphicon-calendar:before{content:"\e109"}.glyphicon-random:before{content:"\e110"}.glyphicon-comment:before{content:"\e111"}.glyphicon-magnet:before{content:"\e112"}.glyphicon-chevron-up:before{content:"\e113"}.glyphicon-chevron-down:before{content:"\e114"}.glyphicon-retweet:before{content:"\e115"}.glyphicon-shopping-cart:before{content:"\e116"}.glyphicon-folder-close:before{content:"\e117"}.glyphicon-folder-open:before{content:"\e118"}.glyphicon-resize-vertical:before{content:"\e119"}.glyphicon-resize-horizontal:before{content:"\e120"}.glyphicon-hdd:before{content:"\e121"}.glyphicon-bullhorn:before{content:"\e122"}.glyphicon-bell:before{content:"\e123"}.glyphicon-certificate:before{content:"\e124"}.glyphicon-thumbs-up:before{content:"\e125"}.glyphicon-thumbs-down:before{content:"\e126"}.glyphicon-hand-right:before{content:"\e127"}.glyphicon-hand-left:before{content:"\e128"}.glyphicon-hand-up:before{content:"\e129"}.glyphicon-hand-down:before{content:"\e130"}.glyphicon-circle-arrow-right:before{content:"\e131"}.glyphicon-circle-arrow-left:before{content:"\e132"}.glyphicon-circle-arrow-up:before{content:"\e133"}.glyphicon-circle-arrow-down:before{content:"\e134"}.glyphicon-globe:before{content:"\e135"}.glyphicon-wrench:before{content:"\e136"}.glyphicon-tasks:before{content:"\e137"}.glyphicon-filter:before{content:"\e138"}.glyphicon-briefcase:before{content:"\e139"}.glyphicon-fullscreen:before{content:"\e140"}.glyphicon-dashboard:before{content:"\e141"}.glyphicon-paperclip:before{content:"\e142"}.glyphicon-heart-empty:before{content:"\e143"}.glyphicon-link:before{content:"\e144"}.glyphicon-phone:before{content:"\e145"}.glyphicon-pushpin:before{content:"\e146"}.glyphicon-usd:before{content:"\e148"}.glyphicon-gbp:before{content:"\e149"}.glyphicon-sort:before{content:"\e150"}.glyphicon-sort-by-alphabet:before{content:"\e151"}.glyphicon-sort-by-alphabet-alt:before{content:"\e152"}.glyphicon-sort-by-order:before{content:"\e153"}.glyphicon-sort-by-order-alt:before{content:"\e154"}.glyphicon-sort-by-attributes:before{content:"\e155"}.glyphicon-sort-by-attributes-alt:before{content:"\e156"}.glyphicon-unchecked:before{content:"\e157"}.glyphicon-expand:before{content:"\e158"}.glyphicon-collapse-down:before{content:"\e159"}.glyphicon-collapse-up:before{content:"\e160"}.glyphicon-log-in:before{content:"\e161"}.glyphicon-flash:before{content:"\e162"}.glyphicon-log-out:before{content:"\e163"}.glyphicon-new-window:before{content:"\e164"}.glyphicon-record:before{content:"\e165"}.glyphicon-save:before{content:"\e166"}.glyphicon-open:before{content:"\e167"}.glyphicon-saved:before{content:"\e168"}.glyphicon-import:before{content:"\e169"}.glyphicon-export:before{content:"\e170"}.glyphicon-send:before{content:"\e171"}.glyphicon-floppy-disk:before{content:"\e172"}.glyphicon-floppy-saved:before{content:"\e173"}.glyphicon-floppy-remove:before{content:"\e174"}.glyphicon-floppy-save:before{content:"\e175"}.glyphicon-floppy-open:before{content:"\e176"}.glyphicon-credit-card:before{content:"\e177"}.glyphicon-transfer:before{content:"\e178"}.glyphicon-cutlery:before{content:"\e179"}.glyphicon-header:before{content:"\e180"}.glyphicon-compressed:before{content:"\e181"}.glyphicon-earphone:before{content:"\e182"}.glyphicon-phone-alt:before{content:"\e183"}.glyphicon-tower:before{content:"\e184"}.glyphicon-stats:before{content:"\e185"}.glyphicon-sd-video:before{content:"\e186"}.glyphicon-hd-video:before{content:"\e187"}.glyphicon-subtitles:before{content:"\e188"}.glyphicon-sound-stereo:before{content:"\e189"}.glyphicon-sound-dolby:before{content:"\e190"}.glyphicon-sound-5-1:before{content:"\e191"}.glyphicon-sound-6-1:before{content:"\e192"}.glyphicon-sound-7-1:before{content:"\e193"}.glyphicon-copyright-mark:before{content:"\e194"}.glyphicon-registration-mark:before{content:"\e195"}.glyphicon-cloud-download:before{content:"\e197"}.glyphicon-cloud-upload:before{content:"\e198"}.glyphicon-tree-conifer:before{content:"\e199"}.glyphicon-tree-deciduous:before{content:"\e200"}.glyphicon-cd:before{content:"\e201"}.glyphicon-save-file:before{content:"\e202"}.glyphicon-open-file:before{content:"\e203"}.glyphicon-level-up:before{content:"\e204"}.glyphicon-copy:before{content:"\e205"}.glyphicon-paste:before{content:"\e206"}.glyphicon-alert:before{content:"\e209"}.glyphicon-equalizer:before{content:"\e210"}.glyphicon-king:before{content:"\e211"}.glyphicon-queen:before{content:"\e212"}.glyphicon-pawn:before{content:"\e213"}.glyphicon-bishop:before{content:"\e214"}.glyphicon-knight:before{content:"\e215"}.glyphicon-baby-formula:before{content:"\e216"}.glyphicon-tent:before{content:"\26fa"}.glyphicon-blackboard:before{content:"\e218"}.glyphicon-bed:before{content:"\e219"}.glyphicon-apple:before{content:"\f8ff"}.glyphicon-erase:before{content:"\e221"}.glyphicon-hourglass:before{content:"\231b"}.glyphicon-lamp:before{content:"\e223"}.glyphicon-duplicate:before{content:"\e224"}.glyphicon-piggy-bank:before{content:"\e225"}.glyphicon-scissors:before{content:"\e226"}.glyphicon-bitcoin:before,.glyphicon-btc:before,.glyphicon-xbt:before{content:"\e227"}.glyphicon-jpy:before,.glyphicon-yen:before{content:"\00a5"}.glyphicon-rub:before,.glyphicon-ruble:before{content:"\20bd"}.glyphicon-scale:before{content:"\e230"}.glyphicon-ice-lolly:before{content:"\e231"}.glyphicon-ice-lolly-tasted:before{content:"\e232"}.glyphicon-education:before{content:"\e233"}.glyphicon-option-horizontal:before{content:"\e234"}.glyphicon-option-vertical:before{content:"\e235"}.glyphicon-menu-hamburger:before{content:"\e236"}.glyphicon-modal-window:before{content:"\e237"}.glyphicon-oil:before{content:"\e238"}.glyphicon-grain:before{content:"\e239"}.glyphicon-sunglasses:before{content:"\e240"}.glyphicon-text-size:before{content:"\e241"}.glyphicon-text-color:before{content:"\e242"}.glyphicon-text-background:before{content:"\e243"}.glyphicon-object-align-top:before{content:"\e244"}.glyphicon-object-align-bottom:before{content:"\e245"}.glyphicon-object-align-horizontal:before{content:"\e246"}.glyphicon-object-align-left:before{content:"\e247"}.glyphicon-object-align-vertical:before{content:"\e248"}.glyphicon-object-align-right:before{content:"\e249"}.glyphicon-triangle-right:before{content:"\e250"}.glyphicon-triangle-left:before{content:"\e251"}.glyphicon-triangle-bottom:before{content:"\e252"}.glyphicon-triangle-top:before{content:"\e253"}.glyphicon-console:before{content:"\e254"}.glyphicon-superscript:before{content:"\e255"}.glyphicon-subscript:before{content:"\e256"}.glyphicon-menu-left:before{content:"\e257"}.glyphicon-menu-right:before{content:"\e258"}.glyphicon-menu-down:before{content:"\e259"}.glyphicon-menu-up:before{content:"\e260"}*,:after,:before{-webkit-box-sizing:border-box;-moz-box-sizing:border-box;box-sizing:border-box}body{margin:0;font-family:"Helvetica Neue",Helvetica,Arial,sans-serif;font-size:13px;line-height:1.42857143;color:#000;background-color:#fff}button,input,select,textarea{font-family:inherit;font-size:inherit;line-height:inherit}a{color:#337ab7;text-decoration:none}a:focus,a:hover{color:#23527c;text-decoration:underline}a:focus{outline:dotted thin;outline:-webkit-focus-ring-color auto 5px;outline-offset:-2px}figure{margin:0}.carousel-inner>.item>a>img,.carousel-inner>.item>img,.img-responsive,.thumbnail a>img,.thumbnail>img{display:block;max-width:100%;height:auto}.img-rounded{border-radius:3px}.img-thumbnail{padding:4px;line-height:1.42857143;background-color:#fff;border:1px solid #ddd;border-radius:2px;-webkit-transition:all .2s ease-in-out;-o-transition:all .2s ease-in-out;transition:all .2s ease-in-out;display:inline-block;max-width:100%;height:auto}.img-circle{border-radius:50%}hr{margin-top:18px;margin-bottom:18px;border:0;border-top:1px solid #eee}.sr-only{position:absolute;width:1px;height:1px;margin:-1px;padding:0;overflow:hidden;clip:rect(0,0,0,0);border:0}.sr-only-focusable:active,.sr-only-focusable:focus{position:static;width:auto;height:auto;margin:0;overflow:visible;clip:auto}[role=button]{cursor:pointer}.h1,.h2,.h3,.h4,.h5,.h6,h1,h2,h3,h4,h5,h6{font-family:inherit;font-weight:500;line-height:1.1;color:inherit}.h1 .small,.h1 small,.h2 .small,.h2 small,.h3 .small,.h3 small,.h4 .small,.h4 small,.h5 .small,.h5 small,.h6 .small,.h6 small,h1 .small,h1 small,h2 .small,h2 small,h3 .small,h3 small,h4 .small,h4 small,h5 .small,h5 small,h6 .small,h6 small{font-weight:400;line-height:1;color:#777}.h1,.h2,.h3,h1,h2,h3{margin-top:18px;margin-bottom:9px}.h1 .small,.h1 small,.h2 .small,.h2 small,.h3 .small,.h3 small,h1 .small,h1 small,h2 .small,h2 small,h3 .small,h3 small{font-size:65%}.h4,.h5,.h6,h4,h5,h6{margin-top:9px;margin-bottom:9px}.h4 .small,.h4 small,.h5 .small,.h5 small,.h6 .small,.h6 small,h4 .small,h4 small,h5 .small,h5 small,h6 .small,h6 small{font-size:75%}.h1,h1{font-size:33px}.h2,h2{font-size:27px}.h3,h3{font-size:23px}.h4,h4{font-size:17px}.h5,h5{font-size:13px}.h6,h6{font-size:12px}p{margin:0 0 9px}.lead{margin-bottom:18px;font-size:14px;font-weight:300;line-height:1.4}@media (min-width:768px){.lead{font-size:19.5px}}.small,small{font-size:92%}.mark,mark{background-color:#fcf8e3;padding:.2em}.text-left{text-align:left}.text-right{text-align:right}.text-center{text-align:center}.text-justify{text-align:justify}.text-nowrap{white-space:nowrap}.text-lowercase{text-transform:lowercase}.text-uppercase{text-transform:uppercase}.text-capitalize{text-transform:capitalize}.text-muted{color:#777}.text-primary{color:#337ab7}a.text-primary:hover{color:#286090}.text-success{color:#3c763d}a.text-success:hover{color:#2b542c}.text-info{color:#31708f}a.text-info:hover{color:#245269}.text-warning{color:#8a6d3b}a.text-warning:hover{color:#66512c}.text-danger{color:#a94442}a.text-danger:hover{color:#843534}.bg-primary{color:#fff;background-color:#337ab7}a.bg-primary:hover{background-color:#286090}.bg-success{background-color:#dff0d8}a.bg-success:hover{background-color:#c1e2b3}.bg-info{background-color:#d9edf7}a.bg-info:hover{background-color:#afd9ee}.bg-warning{background-color:#fcf8e3}a.bg-warning:hover{background-color:#f7ecb5}.bg-danger{background-color:#f2dede}a.bg-danger:hover{background-color:#e4b9b9}.page-header{padding-bottom:8px;margin:36px 0 18px;border-bottom:1px solid #eee}ol,ul{margin-top:0;margin-bottom:9px}ol ol,ol ul,ul ol,ul ul{margin-bottom:0}.list-unstyled{padding-left:0;list-style:none}.list-inline{padding-left:0;list-style:none;margin-left:-5px}.list-inline>li{display:inline-block;padding-left:5px;padding-right:5px}dl{margin-top:0;margin-bottom:18px}dd,dt{line-height:1.42857143}dt{font-weight:700}dd{margin-left:0}@media (min-width:541px){.dl-horizontal dt{float:left;width:160px;clear:left;text-align:right;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}.dl-horizontal dd{margin-left:180px}}abbr[data-original-title],abbr[title]{cursor:help;border-bottom:1px dotted #777}.initialism{font-size:90%;text-transform:uppercase}blockquote{padding:9px 18px;margin:0 0 18px;font-size:inherit;border-left:5px solid #eee}blockquote ol:last-child,blockquote p:last-child,blockquote ul:last-child{margin-bottom:0}blockquote .small,blockquote footer,blockquote small{display:block;font-size:80%;line-height:1.42857143;color:#777}blockquote .small:before,blockquote footer:before,blockquote small:before{content:'\2014 \00A0'}.blockquote-reverse,blockquote.pull-right{padding-right:15px;padding-left:0;border-right:5px solid #eee;border-left:0;text-align:right}.blockquote-reverse .small:before,.blockquote-reverse footer:before,.blockquote-reverse small:before,blockquote.pull-right .small:before,blockquote.pull-right footer:before,blockquote.pull-right small:before{content:''}.blockquote-reverse .small:after,.blockquote-reverse footer:after,.blockquote-reverse small:after,blockquote.pull-right .small:after,blockquote.pull-right footer:after,blockquote.pull-right small:after{content:'\00A0 \2014'}address{margin-bottom:18px;font-style:normal;line-height:1.42857143}code,kbd,pre,samp{font-family:monospace}code{padding:2px 4px;font-size:90%;background-color:#f9f2f4;border-radius:2px}kbd{padding:2px 4px;font-size:90%;color:#fff;background-color:#333;border-radius:1px;box-shadow:inset 0 -1px 0 rgba(0,0,0,.25)}kbd kbd{padding:0;font-size:100%;font-weight:700;box-shadow:none}pre{display:block;padding:8.5px;margin:0 0 9px;word-break:break-all;word-wrap:break-word;color:#333;background-color:#f5f5f5;border:1px solid #ccc;border-radius:2px}pre code{padding:0;font-size:inherit;color:inherit;white-space:pre-wrap;background-color:transparent;border-radius:0}.pre-scrollable{max-height:340px;overflow-y:scroll}.container{margin-right:auto;margin-left:auto;padding-left:0;padding-right:0}@media (min-width:768px){.container{width:768px}}@media (min-width:992px){.container{width:940px}}@media (min-width:1200px){.container{width:1140px}}.container-fluid{margin-right:auto;margin-left:auto;padding-left:0;padding-right:0}.row{margin-left:0;margin-right:0}.col-lg-1,.col-lg-10,.col-lg-11,.col-lg-12,.col-lg-2,.col-lg-3,.col-lg-4,.col-lg-5,.col-lg-6,.col-lg-7,.col-lg-8,.col-lg-9,.col-md-1,.col-md-10,.col-md-11,.col-md-12,.col-md-2,.col-md-3,.col-md-4,.col-md-5,.col-md-6,.col-md-7,.col-md-8,.col-md-9,.col-sm-1,.col-sm-10,.col-sm-11,.col-sm-12,.col-sm-2,.col-sm-3,.col-sm-4,.col-sm-5,.col-sm-6,.col-sm-7,.col-sm-8,.col-sm-9,.col-xs-1,.col-xs-10,.col-xs-11,.col-xs-12,.col-xs-2,.col-xs-3,.col-xs-4,.col-xs-5,.col-xs-6,.col-xs-7,.col-xs-8,.col-xs-9{position:relative;min-height:1px;padding-left:0;padding-right:0}.col-xs-1,.col-xs-10,.col-xs-11,.col-xs-12,.col-xs-2,.col-xs-3,.col-xs-4,.col-xs-5,.col-xs-6,.col-xs-7,.col-xs-8,.col-xs-9{float:left}.col-xs-12{width:100%}.col-xs-11{width:91.66666667%}.col-xs-10{width:83.33333333%}.col-xs-9{width:75%}.col-xs-8{width:66.66666667%}.col-xs-7{width:58.33333333%}.col-xs-6{width:50%}.col-xs-5{width:41.66666667%}.col-xs-4{width:33.33333333%}.col-xs-3{width:25%}.col-xs-2{width:16.66666667%}.col-xs-1{width:8.33333333%}.col-xs-pull-12{right:100%}.col-xs-pull-11{right:91.66666667%}.col-xs-pull-10{right:83.33333333%}.col-xs-pull-9{right:75%}.col-xs-pull-8{right:66.66666667%}.col-xs-pull-7{right:58.33333333%}.col-xs-pull-6{right:50%}.col-xs-pull-5{right:41.66666667%}.col-xs-pull-4{right:33.33333333%}.col-xs-pull-3{right:25%}.col-xs-pull-2{right:16.66666667%}.col-xs-pull-1{right:8.33333333%}.col-xs-pull-0{right:auto}.col-xs-push-12{left:100%}.col-xs-push-11{left:91.66666667%}.col-xs-push-10{left:83.33333333%}.col-xs-push-9{left:75%}.col-xs-push-8{left:66.66666667%}.col-xs-push-7{left:58.33333333%}.col-xs-push-6{left:50%}.col-xs-push-5{left:41.66666667%}.col-xs-push-4{left:33.33333333%}.col-xs-push-3{left:25%}.col-xs-push-2{left:16.66666667%}.col-xs-push-1{left:8.33333333%}.col-xs-push-0{left:auto}.col-xs-offset-12{margin-left:100%}.col-xs-offset-11{margin-left:91.66666667%}.col-xs-offset-10{margin-left:83.33333333%}.col-xs-offset-9{margin-left:75%}.col-xs-offset-8{margin-left:66.66666667%}.col-xs-offset-7{margin-left:58.33333333%}.col-xs-offset-6{margin-left:50%}.col-xs-offset-5{margin-left:41.66666667%}.col-xs-offset-4{margin-left:33.33333333%}.col-xs-offset-3{margin-left:25%}.col-xs-offset-2{margin-left:16.66666667%}.col-xs-offset-1{margin-left:8.33333333%}.col-xs-offset-0{margin-left:0}@media (min-width:768px){.col-sm-1,.col-sm-10,.col-sm-11,.col-sm-12,.col-sm-2,.col-sm-3,.col-sm-4,.col-sm-5,.col-sm-6,.col-sm-7,.col-sm-8,.col-sm-9{float:left}.col-sm-12{width:100%}.col-sm-11{width:91.66666667%}.col-sm-10{width:83.33333333%}.col-sm-9{width:75%}.col-sm-8{width:66.66666667%}.col-sm-7{width:58.33333333%}.col-sm-6{width:50%}.col-sm-5{width:41.66666667%}.col-sm-4{width:33.33333333%}.col-sm-3{width:25%}.col-sm-2{width:16.66666667%}.col-sm-1{width:8.33333333%}.col-sm-pull-12{right:100%}.col-sm-pull-11{right:91.66666667%}.col-sm-pull-10{right:83.33333333%}.col-sm-pull-9{right:75%}.col-sm-pull-8{right:66.66666667%}.col-sm-pull-7{right:58.33333333%}.col-sm-pull-6{right:50%}.col-sm-pull-5{right:41.66666667%}.col-sm-pull-4{right:33.33333333%}.col-sm-pull-3{right:25%}.col-sm-pull-2{right:16.66666667%}.col-sm-pull-1{right:8.33333333%}.col-sm-pull-0{right:auto}.col-sm-push-12{left:100%}.col-sm-push-11{left:91.66666667%}.col-sm-push-10{left:83.33333333%}.col-sm-push-9{left:75%}.col-sm-push-8{left:66.66666667%}.col-sm-push-7{left:58.33333333%}.col-sm-push-6{left:50%}.col-sm-push-5{left:41.66666667%}.col-sm-push-4{left:33.33333333%}.col-sm-push-3{left:25%}.col-sm-push-2{left:16.66666667%}.col-sm-push-1{left:8.33333333%}.col-sm-push-0{left:auto}.col-sm-offset-12{margin-left:100%}.col-sm-offset-11{margin-left:91.66666667%}.col-sm-offset-10{margin-left:83.33333333%}.col-sm-offset-9{margin-left:75%}.col-sm-offset-8{margin-left:66.66666667%}.col-sm-offset-7{margin-left:58.33333333%}.col-sm-offset-6{margin-left:50%}.col-sm-offset-5{margin-left:41.66666667%}.col-sm-offset-4{margin-left:33.33333333%}.col-sm-offset-3{margin-left:25%}.col-sm-offset-2{margin-left:16.66666667%}.col-sm-offset-1{margin-left:8.33333333%}.col-sm-offset-0{margin-left:0}}@media (min-width:992px){.col-md-1,.col-md-10,.col-md-11,.col-md-12,.col-md-2,.col-md-3,.col-md-4,.col-md-5,.col-md-6,.col-md-7,.col-md-8,.col-md-9{float:left}.col-md-12{width:100%}.col-md-11{width:91.66666667%}.col-md-10{width:83.33333333%}.col-md-9{width:75%}.col-md-8{width:66.66666667%}.col-md-7{width:58.33333333%}.col-md-6{width:50%}.col-md-5{width:41.66666667%}.col-md-4{width:33.33333333%}.col-md-3{width:25%}.col-md-2{width:16.66666667%}.col-md-1{width:8.33333333%}.col-md-pull-12{right:100%}.col-md-pull-11{right:91.66666667%}.col-md-pull-10{right:83.33333333%}.col-md-pull-9{right:75%}.col-md-pull-8{right:66.66666667%}.col-md-pull-7{right:58.33333333%}.col-md-pull-6{right:50%}.col-md-pull-5{right:41.66666667%}.col-md-pull-4{right:33.33333333%}.col-md-pull-3{right:25%}.col-md-pull-2{right:16.66666667%}.col-md-pull-1{right:8.33333333%}.col-md-pull-0{right:auto}.col-md-push-12{left:100%}.col-md-push-11{left:91.66666667%}.col-md-push-10{left:83.33333333%}.col-md-push-9{left:75%}.col-md-push-8{left:66.66666667%}.col-md-push-7{left:58.33333333%}.col-md-push-6{left:50%}.col-md-push-5{left:41.66666667%}.col-md-push-4{left:33.33333333%}.col-md-push-3{left:25%}.col-md-push-2{left:16.66666667%}.col-md-push-1{left:8.33333333%}.col-md-push-0{left:auto}.col-md-offset-12{margin-left:100%}.col-md-offset-11{margin-left:91.66666667%}.col-md-offset-10{margin-left:83.33333333%}.col-md-offset-9{margin-left:75%}.col-md-offset-8{margin-left:66.66666667%}.col-md-offset-7{margin-left:58.33333333%}.col-md-offset-6{margin-left:50%}.col-md-offset-5{margin-left:41.66666667%}.col-md-offset-4{margin-left:33.33333333%}.col-md-offset-3{margin-left:25%}.col-md-offset-2{margin-left:16.66666667%}.col-md-offset-1{margin-left:8.33333333%}.col-md-offset-0{margin-left:0}}@media (min-width:1200px){.col-lg-1,.col-lg-10,.col-lg-11,.col-lg-12,.col-lg-2,.col-lg-3,.col-lg-4,.col-lg-5,.col-lg-6,.col-lg-7,.col-lg-8,.col-lg-9{float:left}.col-lg-12{width:100%}.col-lg-11{width:91.66666667%}.col-lg-10{width:83.33333333%}.col-lg-9{width:75%}.col-lg-8{width:66.66666667%}.col-lg-7{width:58.33333333%}.col-lg-6{width:50%}.col-lg-5{width:41.66666667%}.col-lg-4{width:33.33333333%}.col-lg-3{width:25%}.col-lg-2{width:16.66666667%}.col-lg-1{width:8.33333333%}.col-lg-pull-12{right:100%}.col-lg-pull-11{right:91.66666667%}.col-lg-pull-10{right:83.33333333%}.col-lg-pull-9{right:75%}.col-lg-pull-8{right:66.66666667%}.col-lg-pull-7{right:58.33333333%}.col-lg-pull-6{right:50%}.col-lg-pull-5{right:41.66666667%}.col-lg-pull-4{right:33.33333333%}.col-lg-pull-3{right:25%}.col-lg-pull-2{right:16.66666667%}.col-lg-pull-1{right:8.33333333%}.col-lg-pull-0{right:auto}.col-lg-push-12{left:100%}.col-lg-push-11{left:91.66666667%}.col-lg-push-10{left:83.33333333%}.col-lg-push-9{left:75%}.col-lg-push-8{left:66.66666667%}.col-lg-push-7{left:58.33333333%}.col-lg-push-6{left:50%}.col-lg-push-5{left:41.66666667%}.col-lg-push-4{left:33.33333333%}.col-lg-push-3{left:25%}.col-lg-push-2{left:16.66666667%}.col-lg-push-1{left:8.33333333%}.col-lg-push-0{left:auto}.col-lg-offset-12{margin-left:100%}.col-lg-offset-11{margin-left:91.66666667%}.col-lg-offset-10{margin-left:83.33333333%}.col-lg-offset-9{margin-left:75%}.col-lg-offset-8{margin-left:66.66666667%}.col-lg-offset-7{margin-left:58.33333333%}.col-lg-offset-6{margin-left:50%}.col-lg-offset-5{margin-left:41.66666667%}.col-lg-offset-4{margin-left:33.33333333%}.col-lg-offset-3{margin-left:25%}.col-lg-offset-2{margin-left:16.66666667%}.col-lg-offset-1{margin-left:8.33333333%}.col-lg-offset-0{margin-left:0}}table{background-color:transparent}caption{padding-top:8px;padding-bottom:8px;color:#777;text-align:left}th{text-align:left}.table{width:100%;max-width:100%;margin-bottom:18px}.table>tbody>tr>td,.table>tbody>tr>th,.table>tfoot>tr>td,.table>tfoot>tr>th,.table>thead>tr>td,.table>thead>tr>th{padding:8px;line-height:1.42857143;vertical-align:top;border-top:1px solid #ddd}.table>thead>tr>th{vertical-align:bottom;border-bottom:2px solid #ddd}.table>caption+thead>tr:first-child>td,.table>caption+thead>tr:first-child>th,.table>colgroup+thead>tr:first-child>td,.table>colgroup+thead>tr:first-child>th,.table>thead:first-child>tr:first-child>td,.table>thead:first-child>tr:first-child>th{border-top:0}.table>tbody+tbody{border-top:2px solid #ddd}.table .table{background-color:#fff}.table-condensed>tbody>tr>td,.table-condensed>tbody>tr>th,.table-condensed>tfoot>tr>td,.table-condensed>tfoot>tr>th,.table-condensed>thead>tr>td,.table-condensed>thead>tr>th{padding:5px}.table-bordered,.table-bordered>tbody>tr>td,.table-bordered>tbody>tr>th,.table-bordered>tfoot>tr>td,.table-bordered>tfoot>tr>th,.table-bordered>thead>tr>td,.table-bordered>thead>tr>th{border:1px solid #ddd}.table-bordered>thead>tr>td,.table-bordered>thead>tr>th{border-bottom-width:2px}.table-striped>tbody>tr:nth-of-type(odd){background-color:#f9f9f9}.table-hover>tbody>tr:hover{background-color:#f5f5f5}table col[class*=col-]{position:static;float:none;display:table-column}table td[class*=col-],table th[class*=col-]{position:static;float:none;display:table-cell}.table>tbody>tr.active>td,.table>tbody>tr.active>th,.table>tbody>tr>td.active,.table>tbody>tr>th.active,.table>tfoot>tr.active>td,.table>tfoot>tr.active>th,.table>tfoot>tr>td.active,.table>tfoot>tr>th.active,.table>thead>tr.active>td,.table>thead>tr.active>th,.table>thead>tr>td.active,.table>thead>tr>th.active{background-color:#f5f5f5}.table-hover>tbody>tr.active:hover>td,.table-hover>tbody>tr.active:hover>th,.table-hover>tbody>tr:hover>.active,.table-hover>tbody>tr>td.active:hover,.table-hover>tbody>tr>th.active:hover{background-color:#e8e8e8}.table>tbody>tr.success>td,.table>tbody>tr.success>th,.table>tbody>tr>td.success,.table>tbody>tr>th.success,.table>tfoot>tr.success>td,.table>tfoot>tr.success>th,.table>tfoot>tr>td.success,.table>tfoot>tr>th.success,.table>thead>tr.success>td,.table>thead>tr.success>th,.table>thead>tr>td.success,.table>thead>tr>th.success{background-color:#dff0d8}.table-hover>tbody>tr.success:hover>td,.table-hover>tbody>tr.success:hover>th,.table-hover>tbody>tr:hover>.success,.table-hover>tbody>tr>td.success:hover,.table-hover>tbody>tr>th.success:hover{background-color:#d0e9c6}.table>tbody>tr.info>td,.table>tbody>tr.info>th,.table>tbody>tr>td.info,.table>tbody>tr>th.info,.table>tfoot>tr.info>td,.table>tfoot>tr.info>th,.table>tfoot>tr>td.info,.table>tfoot>tr>th.info,.table>thead>tr.info>td,.table>thead>tr.info>th,.table>thead>tr>td.info,.table>thead>tr>th.info{background-color:#d9edf7}.table-hover>tbody>tr.info:hover>td,.table-hover>tbody>tr.info:hover>th,.table-hover>tbody>tr:hover>.info,.table-hover>tbody>tr>td.info:hover,.table-hover>tbody>tr>th.info:hover{background-color:#c4e3f3}.table>tbody>tr.warning>td,.table>tbody>tr.warning>th,.table>tbody>tr>td.warning,.table>tbody>tr>th.warning,.table>tfoot>tr.warning>td,.table>tfoot>tr.warning>th,.table>tfoot>tr>td.warning,.table>tfoot>tr>th.warning,.table>thead>tr.warning>td,.table>thead>tr.warning>th,.table>thead>tr>td.warning,.table>thead>tr>th.warning{background-color:#fcf8e3}.table-hover>tbody>tr.warning:hover>td,.table-hover>tbody>tr.warning:hover>th,.table-hover>tbody>tr:hover>.warning,.table-hover>tbody>tr>td.warning:hover,.table-hover>tbody>tr>th.warning:hover{background-color:#faf2cc}.table>tbody>tr.danger>td,.table>tbody>tr.danger>th,.table>tbody>tr>td.danger,.table>tbody>tr>th.danger,.table>tfoot>tr.danger>td,.table>tfoot>tr.danger>th,.table>tfoot>tr>td.danger,.table>tfoot>tr>th.danger,.table>thead>tr.danger>td,.table>thead>tr.danger>th,.table>thead>tr>td.danger,.table>thead>tr>th.danger{background-color:#f2dede}.table-hover>tbody>tr.danger:hover>td,.table-hover>tbody>tr.danger:hover>th,.table-hover>tbody>tr:hover>.danger,.table-hover>tbody>tr>td.danger:hover,.table-hover>tbody>tr>th.danger:hover{background-color:#ebcccc}.table-responsive{overflow-x:auto;min-height:.01%}@media screen and (max-width:767px){.table-responsive{width:100%;margin-bottom:13.5px;overflow-y:hidden;-ms-overflow-style:-ms-autohiding-scrollbar;border:1px solid #ddd}.table-responsive>.table{margin-bottom:0}.table-responsive>.table>tbody>tr>td,.table-responsive>.table>tbody>tr>th,.table-responsive>.table>tfoot>tr>td,.table-responsive>.table>tfoot>tr>th,.table-responsive>.table>thead>tr>td,.table-responsive>.table>thead>tr>th{white-space:nowrap}.table-responsive>.table-bordered{border:0}.table-responsive>.table-bordered>tbody>tr>td:first-child,.table-responsive>.table-bordered>tbody>tr>th:first-child,.table-responsive>.table-bordered>tfoot>tr>td:first-child,.table-responsive>.table-bordered>tfoot>tr>th:first-child,.table-responsive>.table-bordered>thead>tr>td:first-child,.table-responsive>.table-bordered>thead>tr>th:first-child{border-left:0}.table-responsive>.table-bordered>tbody>tr>td:last-child,.table-responsive>.table-bordered>tbody>tr>th:last-child,.table-responsive>.table-bordered>tfoot>tr>td:last-child,.table-responsive>.table-bordered>tfoot>tr>th:last-child,.table-responsive>.table-bordered>thead>tr>td:last-child,.table-responsive>.table-bordered>thead>tr>th:last-child{border-right:0}.table-responsive>.table-bordered>tbody>tr:last-child>td,.table-responsive>.table-bordered>tbody>tr:last-child>th,.table-responsive>.table-bordered>tfoot>tr:last-child>td,.table-responsive>.table-bordered>tfoot>tr:last-child>th{border-bottom:0}}fieldset{padding:0;margin:0;border:0;min-width:0}legend{display:block;width:100%;padding:0;margin-bottom:18px;font-size:19.5px;line-height:inherit;color:#333;border:0;border-bottom:1px solid #e5e5e5}label{display:inline-block;max-width:100%;margin-bottom:5px}input[type=search]{-webkit-box-sizing:border-box;-moz-box-sizing:border-box;box-sizing:border-box;-webkit-appearance:none}input[type=checkbox],input[type=radio]{margin:4px 0 0;margin-top:1px \9;line-height:normal}input[type=file]{display:block}input[type=range]{display:block;width:100%}select[multiple],select[size]{height:auto}input[type=file]:focus,input[type=checkbox]:focus,input[type=radio]:focus{outline:dotted thin;outline:-webkit-focus-ring-color auto 5px;outline-offset:-2px}output{display:block;padding-top:7px;font-size:13px;line-height:1.42857143;color:#555}.form-control{display:block;width:100%;height:32px;padding:6px 12px;font-size:13px;line-height:1.42857143;color:#555;background-color:#fff;background-image:none;border:1px solid #ccc;border-radius:2px;-webkit-box-shadow:inset 0 1px 1px rgba(0,0,0,.075);box-shadow:inset 0 1px 1px rgba(0,0,0,.075);-webkit-transition:border-color ease-in-out .15s,box-shadow ease-in-out .15s;-o-transition:border-color ease-in-out .15s,box-shadow ease-in-out .15s;transition:border-color ease-in-out .15s,box-shadow ease-in-out .15s}.form-control:focus{border-color:#66afe9;outline:0;-webkit-box-shadow:inset 0 1px 1px rgba(0,0,0,.075),0 0 8px rgba(102,175,233,.6);box-shadow:inset 0 1px 1px rgba(0,0,0,.075),0 0 8px rgba(102,175,233,.6)}.form-control::-moz-placeholder{color:#999;opacity:1}.form-control:-ms-input-placeholder{color:#999}.form-control::-webkit-input-placeholder{color:#999}.form-control[disabled],.form-control[readonly],fieldset[disabled] .form-control{background-color:#eee;opacity:1}.form-control[disabled],fieldset[disabled] .form-control{cursor:not-allowed}textarea.form-control{height:auto}@media screen and (-webkit-min-device-pixel-ratio:0){input[type=date],input[type=time],input[type=datetime-local],input[type=month]{line-height:32px}.input-group-sm input[type=date],.input-group-sm input[type=time],.input-group-sm input[type=datetime-local],.input-group-sm input[type=month],input[type=date].input-sm,input[type=time].input-sm,input[type=datetime-local].input-sm,input[type=month].input-sm{line-height:30px}.input-group-lg input[type=date],.input-group-lg input[type=time],.input-group-lg input[type=datetime-local],.input-group-lg input[type=month],input[type=date].input-lg,input[type=time].input-lg,input[type=datetime-local].input-lg,input[type=month].input-lg{line-height:45px}}.form-group{margin-bottom:15px}.checkbox,.radio{position:relative;display:block;margin-top:10px;margin-bottom:10px}.checkbox label,.radio label{min-height:18px;padding-left:20px;margin-bottom:0;font-weight:400;cursor:pointer}.checkbox input[type=checkbox],.checkbox-inline input[type=checkbox],.radio input[type=radio],.radio-inline input[type=radio]{position:absolute;margin-left:-20px;margin-top:4px \9}.checkbox+.checkbox,.radio+.radio{margin-top:-5px}.checkbox-inline,.radio-inline{position:relative;display:inline-block;padding-left:20px;margin-bottom:0;vertical-align:middle;font-weight:400;cursor:pointer}.checkbox-inline+.checkbox-inline,.radio-inline+.radio-inline{margin-top:0;margin-left:10px}.checkbox-inline.disabled,.checkbox.disabled label,.radio-inline.disabled,.radio.disabled label,fieldset[disabled] .checkbox label,fieldset[disabled] .checkbox-inline,fieldset[disabled] .radio label,fieldset[disabled] .radio-inline,fieldset[disabled] input[type=checkbox],fieldset[disabled] input[type=radio],input[type=checkbox].disabled,input[type=checkbox][disabled],input[type=radio].disabled,input[type=radio][disabled]{cursor:not-allowed}.form-control-static{padding-top:7px;padding-bottom:7px;margin-bottom:0;min-height:31px}.form-control-static.input-lg,.form-control-static.input-sm{padding-left:0;padding-right:0}.input-sm{height:30px;padding:5px 10px;font-size:12px;line-height:1.5;border-radius:1px}select.input-sm{height:30px;line-height:30px}select[multiple].input-sm,textarea.input-sm{height:auto}.form-group-sm .form-control{height:30px;padding:5px 10px;font-size:12px;line-height:1.5;border-radius:1px}select.form-group-sm .form-control{height:30px;line-height:30px}select[multiple].form-group-sm .form-control,textarea.form-group-sm .form-control{height:auto}.form-group-sm .form-control-static{height:30px;padding:5px 10px;font-size:12px;line-height:1.5;min-height:30px}.input-lg{height:45px;padding:10px 16px;font-size:17px;line-height:1.3333333;border-radius:3px}select.input-lg{height:45px;line-height:45px}select[multiple].input-lg,textarea.input-lg{height:auto}.form-group-lg .form-control{height:45px;padding:10px 16px;font-size:17px;line-height:1.3333333;border-radius:3px}select.form-group-lg .form-control{height:45px;line-height:45px}select[multiple].form-group-lg .form-control,textarea.form-group-lg .form-control{height:auto}.form-group-lg .form-control-static{height:45px;padding:10px 16px;font-size:17px;line-height:1.3333333;min-height:35px}.has-feedback{position:relative}.has-feedback .form-control{padding-right:40px}.form-control-feedback{position:absolute;top:0;right:0;z-index:2;display:block;width:32px;height:32px;line-height:32px;text-align:center;pointer-events:none}.input-lg+.form-control-feedback{width:45px;height:45px;line-height:45px}.input-sm+.form-control-feedback{width:30px;height:30px;line-height:30px}.has-success .checkbox,.has-success .checkbox-inline,.has-success .control-label,.has-success .help-block,.has-success .radio,.has-success .radio-inline,.has-success.checkbox label,.has-success.checkbox-inline label,.has-success.radio label,.has-success.radio-inline label{color:#3c763d}.has-success .form-control{border-color:#3c763d;-webkit-box-shadow:inset 0 1px 1px rgba(0,0,0,.075);box-shadow:inset 0 1px 1px rgba(0,0,0,.075)}.has-success .form-control:focus{border-color:#2b542c;-webkit-box-shadow:inset 0 1px 1px rgba(0,0,0,.075),0 0 6px #67b168;box-shadow:inset 0 1px 1px rgba(0,0,0,.075),0 0 6px #67b168}.has-success .input-group-addon{color:#3c763d;border-color:#3c763d;background-color:#dff0d8}.has-success .form-control-feedback{color:#3c763d}.has-warning .checkbox,.has-warning .checkbox-inline,.has-warning .control-label,.has-warning .help-block,.has-warning .radio,.has-warning .radio-inline,.has-warning.checkbox label,.has-warning.checkbox-inline label,.has-warning.radio label,.has-warning.radio-inline label{color:#8a6d3b}.has-warning .form-control{border-color:#8a6d3b;-webkit-box-shadow:inset 0 1px 1px rgba(0,0,0,.075);box-shadow:inset 0 1px 1px rgba(0,0,0,.075)}.has-warning .form-control:focus{border-color:#66512c;-webkit-box-shadow:inset 0 1px 1px rgba(0,0,0,.075),0 0 6px #c0a16b;box-shadow:inset 0 1px 1px rgba(0,0,0,.075),0 0 6px #c0a16b}.has-warning .input-group-addon{color:#8a6d3b;border-color:#8a6d3b;background-color:#fcf8e3}.has-warning .form-control-feedback{color:#8a6d3b}.has-error .checkbox,.has-error .checkbox-inline,.has-error .control-label,.has-error .help-block,.has-error .radio,.has-error .radio-inline,.has-error.checkbox label,.has-error.checkbox-inline label,.has-error.radio label,.has-error.radio-inline label{color:#a94442}.has-error .form-control{border-color:#a94442;-webkit-box-shadow:inset 0 1px 1px rgba(0,0,0,.075);box-shadow:inset 0 1px 1px rgba(0,0,0,.075)}.has-error .form-control:focus{border-color:#843534;-webkit-box-shadow:inset 0 1px 1px rgba(0,0,0,.075),0 0 6px #ce8483;box-shadow:inset 0 1px 1px rgba(0,0,0,.075),0 0 6px #ce8483}.has-error .input-group-addon{color:#a94442;border-color:#a94442;background-color:#f2dede}.has-error .form-control-feedback{color:#a94442}.has-feedback label~.form-control-feedback{top:23px}.has-feedback label.sr-only~.form-control-feedback{top:0}.help-block{display:block;margin-top:5px;margin-bottom:10px;color:#404040}.form-horizontal .checkbox,.form-horizontal .checkbox-inline,.form-horizontal .radio,.form-horizontal .radio-inline{margin-top:0;margin-bottom:0;padding-top:7px}.form-horizontal .checkbox,.form-horizontal .radio{min-height:25px}.form-horizontal .form-group{margin-left:0;margin-right:0}.form-horizontal .has-feedback .form-control-feedback{right:0}@media (min-width:768px){.form-inline .form-group{display:inline-block;margin-bottom:0;vertical-align:middle}.form-inline .form-control{display:inline-block;width:auto;vertical-align:middle}.form-inline .form-control-static{display:inline-block}.form-inline .input-group{display:inline-table;vertical-align:middle}.form-inline .input-group .form-control,.form-inline .input-group .input-group-addon,.form-inline .input-group .input-group-btn{width:auto}.form-inline .input-group>.form-control{width:100%}.form-inline .control-label{margin-bottom:0;vertical-align:middle}.form-inline .checkbox,.form-inline .radio{display:inline-block;margin-top:0;margin-bottom:0;vertical-align:middle}.form-inline .checkbox label,.form-inline .radio label{padding-left:0}.form-inline .checkbox input[type=checkbox],.form-inline .radio input[type=radio]{position:relative;margin-left:0}.form-inline .has-feedback .form-control-feedback{top:0}.form-horizontal .control-label{text-align:right;margin-bottom:0;padding-top:7px}.form-horizontal .form-group-lg .control-label{padding-top:14.33px}.form-horizontal .form-group-sm .control-label{padding-top:6px}}.btn{display:inline-block;margin-bottom:0;font-weight:400;text-align:center;vertical-align:middle;touch-action:manipulation;cursor:pointer;background-image:none;border:1px solid transparent;white-space:nowrap;padding:6px 12px;font-size:13px;line-height:1.42857143;border-radius:2px;-webkit-user-select:none;-moz-user-select:none;-ms-user-select:none;user-select:none}.btn.active.focus,.btn.active:focus,.btn.focus,.btn:active.focus,.btn:active:focus,.btn:focus{outline:dotted thin;outline:-webkit-focus-ring-color auto 5px;outline-offset:-2px}.btn.focus,.btn:focus,.btn:hover{color:#333;text-decoration:none}.btn.active,.btn:active{outline:0;background-image:none;-webkit-box-shadow:inset 0 3px 5px rgba(0,0,0,.125);box-shadow:inset 0 3px 5px rgba(0,0,0,.125)}.btn.disabled,.btn[disabled],fieldset[disabled] .btn{cursor:not-allowed;pointer-events:none;opacity:.65;filter:alpha(opacity=65);-webkit-box-shadow:none;box-shadow:none}.btn-default{color:#333;background-color:#fff;border-color:#ccc}.btn-default.active,.btn-default.focus,.btn-default:active,.btn-default:focus,.btn-default:hover,.open>.dropdown-toggle.btn-default{color:#333;background-color:#e6e6e6;border-color:#adadad}.btn-default.active,.btn-default:active,.open>.dropdown-toggle.btn-default{background-image:none}.btn-default.disabled,.btn-default.disabled.active,.btn-default.disabled.focus,.btn-default.disabled:active,.btn-default.disabled:focus,.btn-default.disabled:hover,.btn-default[disabled],.btn-default[disabled].active,.btn-default[disabled].focus,.btn-default[disabled]:active,.btn-default[disabled]:focus,.btn-default[disabled]:hover,fieldset[disabled] .btn-default,fieldset[disabled] .btn-default.active,fieldset[disabled] .btn-default.focus,fieldset[disabled] .btn-default:active,fieldset[disabled] .btn-default:focus,fieldset[disabled] .btn-default:hover{background-color:#fff;border-color:#ccc}.btn-default .badge{color:#fff;background-color:#333}.btn-primary{color:#fff;background-color:#337ab7;border-color:#2e6da4}.btn-primary.active,.btn-primary.focus,.btn-primary:active,.btn-primary:focus,.btn-primary:hover,.open>.dropdown-toggle.btn-primary{color:#fff;background-color:#286090;border-color:#204d74}.btn-primary.active,.btn-primary:active,.open>.dropdown-toggle.btn-primary{background-image:none}.btn-primary.disabled,.btn-primary.disabled.active,.btn-primary.disabled.focus,.btn-primary.disabled:active,.btn-primary.disabled:focus,.btn-primary.disabled:hover,.btn-primary[disabled],.btn-primary[disabled].active,.btn-primary[disabled].focus,.btn-primary[disabled]:active,.btn-primary[disabled]:focus,.btn-primary[disabled]:hover,fieldset[disabled] .btn-primary,fieldset[disabled] .btn-primary.active,fieldset[disabled] .btn-primary.focus,fieldset[disabled] .btn-primary:active,fieldset[disabled] .btn-primary:focus,fieldset[disabled] .btn-primary:hover{background-color:#337ab7;border-color:#2e6da4}.btn-primary .badge{color:#337ab7;background-color:#fff}.btn-success{color:#fff;background-color:#5cb85c;border-color:#4cae4c}.btn-success.active,.btn-success.focus,.btn-success:active,.btn-success:focus,.btn-success:hover,.open>.dropdown-toggle.btn-success{color:#fff;background-color:#449d44;border-color:#398439}.btn-success.active,.btn-success:active,.open>.dropdown-toggle.btn-success{background-image:none}.btn-success.disabled,.btn-success.disabled.active,.btn-success.disabled.focus,.btn-success.disabled:active,.btn-success.disabled:focus,.btn-success.disabled:hover,.btn-success[disabled],.btn-success[disabled].active,.btn-success[disabled].focus,.btn-success[disabled]:active,.btn-success[disabled]:focus,.btn-success[disabled]:hover,fieldset[disabled] .btn-success,fieldset[disabled] .btn-success.active,fieldset[disabled] .btn-success.focus,fieldset[disabled] .btn-success:active,fieldset[disabled] .btn-success:focus,fieldset[disabled] .btn-success:hover{background-color:#5cb85c;border-color:#4cae4c}.btn-success .badge{color:#5cb85c;background-color:#fff}.btn-info{color:#fff;background-color:#5bc0de;border-color:#46b8da}.btn-info.active,.btn-info.focus,.btn-info:active,.btn-info:focus,.btn-info:hover,.open>.dropdown-toggle.btn-info{color:#fff;background-color:#31b0d5;border-color:#269abc}.btn-info.active,.btn-info:active,.open>.dropdown-toggle.btn-info{background-image:none}.btn-info.disabled,.btn-info.disabled.active,.btn-info.disabled.focus,.btn-info.disabled:active,.btn-info.disabled:focus,.btn-info.disabled:hover,.btn-info[disabled],.btn-info[disabled].active,.btn-info[disabled].focus,.btn-info[disabled]:active,.btn-info[disabled]:focus,.btn-info[disabled]:hover,fieldset[disabled] .btn-info,fieldset[disabled] .btn-info.active,fieldset[disabled] .btn-info.focus,fieldset[disabled] .btn-info:active,fieldset[disabled] .btn-info:focus,fieldset[disabled] .btn-info:hover{background-color:#5bc0de;border-color:#46b8da}.btn-info .badge{color:#5bc0de;background-color:#fff}.btn-warning{color:#fff;background-color:#f0ad4e;border-color:#eea236}.btn-warning.active,.btn-warning.focus,.btn-warning:active,.btn-warning:focus,.btn-warning:hover,.open>.dropdown-toggle.btn-warning{color:#fff;background-color:#ec971f;border-color:#d58512}.btn-warning.active,.btn-warning:active,.open>.dropdown-toggle.btn-warning{background-image:none}.btn-warning.disabled,.btn-warning.disabled.active,.btn-warning.disabled.focus,.btn-warning.disabled:active,.btn-warning.disabled:focus,.btn-warning.disabled:hover,.btn-warning[disabled],.btn-warning[disabled].active,.btn-warning[disabled].focus,.btn-warning[disabled]:active,.btn-warning[disabled]:focus,.btn-warning[disabled]:hover,fieldset[disabled] .btn-warning,fieldset[disabled] .btn-warning.active,fieldset[disabled] .btn-warning.focus,fieldset[disabled] .btn-warning:active,fieldset[disabled] .btn-warning:focus,fieldset[disabled] .btn-warning:hover{background-color:#f0ad4e;border-color:#eea236}.btn-warning .badge{color:#f0ad4e;background-color:#fff}.btn-danger{color:#fff;background-color:#d9534f;border-color:#d43f3a}.btn-danger.active,.btn-danger.focus,.btn-danger:active,.btn-danger:focus,.btn-danger:hover,.open>.dropdown-toggle.btn-danger{color:#fff;background-color:#c9302c;border-color:#ac2925}.btn-danger.active,.btn-danger:active,.open>.dropdown-toggle.btn-danger{background-image:none}.btn-danger.disabled,.btn-danger.disabled.active,.btn-danger.disabled.focus,.btn-danger.disabled:active,.btn-danger.disabled:focus,.btn-danger.disabled:hover,.btn-danger[disabled],.btn-danger[disabled].active,.btn-danger[disabled].focus,.btn-danger[disabled]:active,.btn-danger[disabled]:focus,.btn-danger[disabled]:hover,fieldset[disabled] .btn-danger,fieldset[disabled] .btn-danger.active,fieldset[disabled] .btn-danger.focus,fieldset[disabled] .btn-danger:active,fieldset[disabled] .btn-danger:focus,fieldset[disabled] .btn-danger:hover{background-color:#d9534f;border-color:#d43f3a}.btn-danger .badge{color:#d9534f;background-color:#fff}.btn-link{color:#337ab7;font-weight:400;border-radius:0}.btn-link,.btn-link.active,.btn-link:active,.btn-link[disabled],fieldset[disabled] .btn-link{background-color:transparent;-webkit-box-shadow:none;box-shadow:none}.btn-link,.btn-link:active,.btn-link:focus,.btn-link:hover{border-color:transparent}.btn-link:focus,.btn-link:hover{color:#23527c;text-decoration:underline;background-color:transparent}.btn-link[disabled]:focus,.btn-link[disabled]:hover,fieldset[disabled] .btn-link:focus,fieldset[disabled] .btn-link:hover{color:#777;text-decoration:none}.btn-group-lg>.btn,.btn-lg{padding:10px 16px;font-size:17px;line-height:1.3333333;border-radius:3px}.btn-group-sm>.btn,.btn-sm{padding:5px 10px;font-size:12px;line-height:1.5;border-radius:1px}.btn-group-xs>.btn,.btn-xs{padding:1px 5px;font-size:12px;line-height:1.5;border-radius:1px}.btn-block{display:block;width:100%}.btn-block+.btn-block{margin-top:5px}input[type=button].btn-block,input[type=reset].btn-block,input[type=submit].btn-block{width:100%}.fade{opacity:0;-webkit-transition:opacity .15s linear;-o-transition:opacity .15s linear;transition:opacity .15s linear}.fade.in{opacity:1}.collapse{display:none}.collapse.in{display:block}tr.collapse.in{display:table-row}tbody.collapse.in{display:table-row-group}.collapsing{position:relative;height:0;overflow:hidden;-webkit-transition-property:height,visibility;transition-property:height,visibility;-webkit-transition-duration:.35s;transition-duration:.35s;-webkit-transition-timing-function:ease;transition-timing-function:ease}.caret{display:inline-block;width:0;height:0;margin-left:2px;vertical-align:middle;border-top:4px dashed;border-right:4px solid transparent;border-left:4px solid transparent}.dropdown,.dropup{position:relative}.dropdown-toggle:focus{outline:0}.dropdown-menu{position:absolute;top:100%;left:0;z-index:1000;display:none;float:left;min-width:160px;padding:5px 0;margin:2px 0 0;list-style:none;font-size:13px;text-align:left;background-color:#fff;border:1px solid #ccc;border:1px solid rgba(0,0,0,.15);border-radius:2px;-webkit-box-shadow:0 6px 12px rgba(0,0,0,.175);box-shadow:0 6px 12px rgba(0,0,0,.175);background-clip:padding-box}.dropdown-menu.pull-right{right:0;left:auto}.dropdown-menu .divider{height:1px;margin:8px 0;overflow:hidden;background-color:#e5e5e5}.dropdown-menu>li>a{display:block;padding:3px 20px;clear:both;font-weight:400;line-height:1.42857143;color:#333;white-space:nowrap}.dropdown-menu>li>a:focus,.dropdown-menu>li>a:hover{text-decoration:none;color:#262626;background-color:#f5f5f5}.dropdown-menu>.active>a,.dropdown-menu>.active>a:focus,.dropdown-menu>.active>a:hover{color:#fff;text-decoration:none;outline:0;background-color:#337ab7}.dropdown-menu>.disabled>a,.dropdown-menu>.disabled>a:focus,.dropdown-menu>.disabled>a:hover{color:#777}.dropdown-menu>.disabled>a:focus,.dropdown-menu>.disabled>a:hover{text-decoration:none;background-color:transparent;background-image:none;filter:progid:DXImageTransform.Microsoft.gradient(enabled=false);cursor:not-allowed}.open>.dropdown-menu{display:block}.open>a{outline:0}.dropdown-menu-right{left:auto;right:0}.dropdown-menu-left{left:0;right:auto}.dropdown-header{display:block;padding:3px 20px;font-size:12px;line-height:1.42857143;color:#777;white-space:nowrap}.dropdown-backdrop{position:fixed;left:0;right:0;bottom:0;top:0;z-index:990}.pull-right>.dropdown-menu{right:0;left:auto}.dropup .caret,.navbar-fixed-bottom .dropdown .caret{border-top:0;border-bottom:4px solid;content:""}.dropup .dropdown-menu,.navbar-fixed-bottom .dropdown .dropdown-menu{top:auto;bottom:100%;margin-bottom:2px}@media (min-width:541px){.navbar-right .dropdown-menu{left:auto;right:0}.navbar-right .dropdown-menu-left{left:0;right:auto}}.btn-group,.btn-group-vertical{position:relative;display:inline-block;vertical-align:middle}.btn-group-vertical>.btn,.btn-group>.btn{position:relative;float:left}.btn-group-vertical>.btn.active,.btn-group-vertical>.btn:active,.btn-group-vertical>.btn:focus,.btn-group-vertical>.btn:hover,.btn-group>.btn.active,.btn-group>.btn:active,.btn-group>.btn:focus,.btn-group>.btn:hover{z-index:2}.btn-group .btn+.btn,.btn-group .btn+.btn-group,.btn-group .btn-group+.btn,.btn-group .btn-group+.btn-group{margin-left:-1px}.btn-toolbar{margin-left:-5px}.btn-toolbar .btn-group,.btn-toolbar .input-group{float:left}.btn-toolbar>.btn,.btn-toolbar>.btn-group,.btn-toolbar>.input-group{margin-left:5px}.btn-group>.btn:not(:first-child):not(:last-child):not(.dropdown-toggle){border-radius:0}.btn-group>.btn:first-child{margin-left:0}.btn-group>.btn:first-child:not(:last-child):not(.dropdown-toggle){border-bottom-right-radius:0;border-top-right-radius:0}.btn-group>.btn:last-child:not(:first-child),.btn-group>.dropdown-toggle:not(:first-child){border-bottom-left-radius:0;border-top-left-radius:0}.btn-group>.btn-group{float:left}.btn-group>.btn-group:not(:first-child):not(:last-child)>.btn{border-radius:0}.btn-group>.btn-group:first-child:not(:last-child)>.btn:last-child,.btn-group>.btn-group:first-child:not(:last-child)>.dropdown-toggle{border-bottom-right-radius:0;border-top-right-radius:0}.btn-group>.btn-group:last-child:not(:first-child)>.btn:first-child{border-bottom-left-radius:0;border-top-left-radius:0}.btn-group .dropdown-toggle:active,.btn-group.open .dropdown-toggle{outline:0}.btn-group>.btn+.dropdown-toggle{padding-left:8px;padding-right:8px}.btn-group>.btn-lg+.dropdown-toggle{padding-left:12px;padding-right:12px}.btn-group.open .dropdown-toggle{-webkit-box-shadow:inset 0 3px 5px rgba(0,0,0,.125);box-shadow:inset 0 3px 5px rgba(0,0,0,.125)}.btn-group.open .dropdown-toggle.btn-link{-webkit-box-shadow:none;box-shadow:none}.btn .caret{margin-left:0}.btn-lg .caret{border-width:5px 5px 0}.dropup .btn-lg .caret{border-width:0 5px 5px}.btn-group-vertical>.btn,.btn-group-vertical>.btn-group,.btn-group-vertical>.btn-group>.btn{display:block;float:none;width:100%;max-width:100%}.btn-group-vertical>.btn-group>.btn{float:none}.btn-group-vertical>.btn+.btn,.btn-group-vertical>.btn+.btn-group,.btn-group-vertical>.btn-group+.btn,.btn-group-vertical>.btn-group+.btn-group{margin-top:-1px;margin-left:0}.btn-group-vertical>.btn:not(:first-child):not(:last-child){border-radius:0}.btn-group-vertical>.btn:first-child:not(:last-child){border-top-right-radius:2px;border-bottom-right-radius:0;border-bottom-left-radius:0}.btn-group-vertical>.btn:last-child:not(:first-child){border-bottom-left-radius:2px;border-top-right-radius:0;border-top-left-radius:0}.btn-group-vertical>.btn-group:not(:first-child):not(:last-child)>.btn{border-radius:0}.btn-group-vertical>.btn-group:first-child:not(:last-child)>.btn:last-child,.btn-group-vertical>.btn-group:first-child:not(:last-child)>.dropdown-toggle{border-bottom-right-radius:0;border-bottom-left-radius:0}.btn-group-vertical>.btn-group:last-child:not(:first-child)>.btn:first-child{border-top-right-radius:0;border-top-left-radius:0}.btn-group-justified{display:table;width:100%;table-layout:fixed;border-collapse:separate}.btn-group-justified>.btn,.btn-group-justified>.btn-group{float:none;display:table-cell;width:1%}.btn-group-justified>.btn-group .btn{width:100%}.btn-group-justified>.btn-group .dropdown-menu{left:auto}[data-toggle=buttons]>.btn input[type=checkbox],[data-toggle=buttons]>.btn input[type=radio],[data-toggle=buttons]>.btn-group>.btn input[type=checkbox],[data-toggle=buttons]>.btn-group>.btn input[type=radio]{position:absolute;clip:rect(0,0,0,0);pointer-events:none}.input-group{position:relative;display:table;border-collapse:separate}.input-group[class*=col-]{float:none;padding-left:0;padding-right:0}.input-group .form-control{position:relative;z-index:2;float:left;width:100%;margin-bottom:0}.input-group-lg>.form-control,.input-group-lg>.input-group-addon,.input-group-lg>.input-group-btn>.btn{height:45px;padding:10px 16px;font-size:17px;line-height:1.3333333;border-radius:3px}select.input-group-lg>.form-control,select.input-group-lg>.input-group-addon,select.input-group-lg>.input-group-btn>.btn{height:45px;line-height:45px}select[multiple].input-group-lg>.form-control,select[multiple].input-group-lg>.input-group-addon,select[multiple].input-group-lg>.input-group-btn>.btn,textarea.input-group-lg>.form-control,textarea.input-group-lg>.input-group-addon,textarea.input-group-lg>.input-group-btn>.btn{height:auto}.input-group-sm>.form-control,.input-group-sm>.input-group-addon,.input-group-sm>.input-group-btn>.btn{height:30px;padding:5px 10px;font-size:12px;line-height:1.5;border-radius:1px}select.input-group-sm>.form-control,select.input-group-sm>.input-group-addon,select.input-group-sm>.input-group-btn>.btn{height:30px;line-height:30px}select[multiple].input-group-sm>.form-control,select[multiple].input-group-sm>.input-group-addon,select[multiple].input-group-sm>.input-group-btn>.btn,textarea.input-group-sm>.form-control,textarea.input-group-sm>.input-group-addon,textarea.input-group-sm>.input-group-btn>.btn{height:auto}.input-group .form-control,.input-group-addon,.input-group-btn{display:table-cell}.input-group .form-control:not(:first-child):not(:last-child),.input-group-addon:not(:first-child):not(:last-child),.input-group-btn:not(:first-child):not(:last-child){border-radius:0}.input-group-addon,.input-group-btn{width:1%;white-space:nowrap;vertical-align:middle}.input-group-addon{padding:6px 12px;font-size:13px;font-weight:400;line-height:1;color:#555;text-align:center;background-color:#eee;border:1px solid #ccc;border-radius:2px}.input-group-addon.input-sm{padding:5px 10px;font-size:12px;border-radius:1px}.input-group-addon.input-lg{padding:10px 16px;font-size:17px;border-radius:3px}.input-group-addon input[type=checkbox],.input-group-addon input[type=radio]{margin-top:0}.input-group .form-control:first-child,.input-group-addon:first-child,.input-group-btn:first-child>.btn,.input-group-btn:first-child>.btn-group>.btn,.input-group-btn:first-child>.dropdown-toggle,.input-group-btn:last-child>.btn-group:not(:last-child)>.btn,.input-group-btn:last-child>.btn:not(:last-child):not(.dropdown-toggle){border-bottom-right-radius:0;border-top-right-radius:0}.input-group-addon:first-child{border-right:0}.input-group .form-control:last-child,.input-group-addon:last-child,.input-group-btn:first-child>.btn-group:not(:first-child)>.btn,.input-group-btn:first-child>.btn:not(:first-child),.input-group-btn:last-child>.btn,.input-group-btn:last-child>.btn-group>.btn,.input-group-btn:last-child>.dropdown-toggle{border-bottom-left-radius:0;border-top-left-radius:0}.input-group-addon:last-child{border-left:0}.input-group-btn{position:relative;font-size:0;white-space:nowrap}.input-group-btn>.btn{position:relative}.input-group-btn>.btn+.btn{margin-left:-1px}.input-group-btn>.btn:active,.input-group-btn>.btn:focus,.input-group-btn>.btn:hover{z-index:2}.input-group-btn:first-child>.btn,.input-group-btn:first-child>.btn-group{margin-right:-1px}.input-group-btn:last-child>.btn,.input-group-btn:last-child>.btn-group{margin-left:-1px}.nav{margin-bottom:0;padding-left:0;list-style:none}.nav>li{position:relative;display:block}.nav>li>a{position:relative;display:block;padding:10px 15px}.nav>li>a:focus,.nav>li>a:hover{text-decoration:none;background-color:#eee}.nav>li.disabled>a{color:#777}.nav>li.disabled>a:focus,.nav>li.disabled>a:hover{color:#777;text-decoration:none;background-color:transparent;cursor:not-allowed}.nav .open>a,.nav .open>a:focus,.nav .open>a:hover{background-color:#eee;border-color:#337ab7}.nav .nav-divider{height:1px;margin:8px 0;overflow:hidden;background-color:#e5e5e5}.nav>li>a>img{max-width:none}.nav-tabs{border-bottom:1px solid #ddd}.nav-tabs>li{float:left;margin-bottom:-1px}.nav-tabs>li>a{margin-right:2px;line-height:1.42857143;border:1px solid transparent;border-radius:2px 2px 0 0}.nav-tabs>li>a:hover{border-color:#eee #eee #ddd}.nav-tabs>li.active>a,.nav-tabs>li.active>a:focus,.nav-tabs>li.active>a:hover{color:#555;background-color:#fff;border:1px solid #ddd;border-bottom-color:transparent;cursor:default}.nav-tabs.nav-justified{width:100%;border-bottom:0}.nav-tabs.nav-justified>li{float:none}.nav-tabs.nav-justified>li>a{text-align:center;margin-bottom:5px;margin-right:0;border-radius:2px}.nav-tabs.nav-justified>.dropdown .dropdown-menu{top:auto;left:auto}.nav-tabs.nav-justified>.active>a,.nav-tabs.nav-justified>.active>a:focus,.nav-tabs.nav-justified>.active>a:hover{border:1px solid #ddd}@media (min-width:768px){.nav-tabs.nav-justified>li{display:table-cell;width:1%}.nav-tabs.nav-justified>li>a{margin-bottom:0;border-bottom:1px solid #ddd;border-radius:2px 2px 0 0}.nav-tabs.nav-justified>.active>a,.nav-tabs.nav-justified>.active>a:focus,.nav-tabs.nav-justified>.active>a:hover{border-bottom-color:#fff}}.nav-pills>li{float:left}.nav-pills>li>a{border-radius:2px}.nav-pills>li+li{margin-left:2px}.nav-pills>li.active>a,.nav-pills>li.active>a:focus,.nav-pills>li.active>a:hover{color:#fff;background-color:#337ab7}.nav-stacked>li{float:none}.nav-stacked>li+li{margin-top:2px;margin-left:0}.nav-justified{width:100%}.nav-justified>li{float:none}.nav-justified>li>a{text-align:center;margin-bottom:5px}.nav-justified>.dropdown .dropdown-menu{top:auto;left:auto}.nav-tabs-justified{border-bottom:0}.nav-tabs-justified>li>a{margin-right:0;border-radius:2px}.nav-tabs-justified>.active>a,.nav-tabs-justified>.active>a:focus,.nav-tabs-justified>.active>a:hover{border:1px solid #ddd}@media (min-width:768px){.nav-justified>li{display:table-cell;width:1%}.nav-justified>li>a{margin-bottom:0}.nav-tabs-justified>li>a{border-bottom:1px solid #ddd;border-radius:2px 2px 0 0}.nav-tabs-justified>.active>a,.nav-tabs-justified>.active>a:focus,.nav-tabs-justified>.active>a:hover{border-bottom-color:#fff}}.tab-content>.tab-pane{display:none}.tab-content>.active{display:block}.nav-tabs .dropdown-menu{margin-top:-1px;border-top-right-radius:0;border-top-left-radius:0}.navbar{position:relative;min-height:30px;margin-bottom:18px;border:1px solid transparent}.navbar-collapse{overflow-x:visible;padding-right:0;padding-left:0;border-top:1px solid transparent;box-shadow:inset 0 1px 0 rgba(255,255,255,.1);-webkit-overflow-scrolling:touch}.navbar-collapse.in{overflow-y:auto}.navbar-fixed-bottom .navbar-collapse,.navbar-fixed-top .navbar-collapse{max-height:340px}@media (max-device-width:540px)and (orientation:landscape){.navbar-fixed-bottom .navbar-collapse,.navbar-fixed-top .navbar-collapse{max-height:200px}}.container-fluid>.navbar-collapse,.container-fluid>.navbar-header,.container>.navbar-collapse,.container>.navbar-header{margin-right:0;margin-left:0}.navbar-static-top{z-index:1000;border-width:0 0 1px}.navbar-fixed-bottom,.navbar-fixed-top{position:fixed;right:0;left:0;z-index:1030}@media (min-width:541px){.navbar{border-radius:2px}.navbar-header{float:left}.navbar-collapse{width:auto;border-top:0;box-shadow:none}.navbar-collapse.collapse{display:block!important;height:auto!important;padding-bottom:0;overflow:visible!important}.navbar-collapse.in{overflow-y:visible}.navbar-fixed-bottom .navbar-collapse,.navbar-fixed-top .navbar-collapse,.navbar-static-top .navbar-collapse{padding-left:0;padding-right:0}.container-fluid>.navbar-collapse,.container-fluid>.navbar-header,.container>.navbar-collapse,.container>.navbar-header{margin-right:0;margin-left:0}.navbar-fixed-bottom,.navbar-fixed-top,.navbar-static-top{border-radius:0}}.navbar-fixed-top{top:0;border-width:0 0 1px}.navbar-fixed-bottom{bottom:0;margin-bottom:0;border-width:1px 0 0}.navbar-brand{float:left;padding:6px 0;font-size:17px;line-height:18px;height:30px}.navbar-brand:focus,.navbar-brand:hover{text-decoration:none}.navbar-brand>img{display:block}.navbar-toggle{position:relative;float:right;margin-right:0;padding:9px 10px;margin-top:-2px;margin-bottom:-2px;background-color:transparent;background-image:none;border:1px solid transparent;border-radius:2px}.navbar-toggle:focus{outline:0}.navbar-toggle .icon-bar{display:block;width:22px;height:2px;border-radius:1px}.navbar-toggle .icon-bar+.icon-bar{margin-top:4px}@media (min-width:541px){.navbar>.container .navbar-brand,.navbar>.container-fluid .navbar-brand{margin-left:0}.navbar-toggle{display:none}}.navbar-nav{margin:3px 0}.navbar-nav>li>a{padding-top:10px;padding-bottom:10px;line-height:18px}@media (max-width:540px){.navbar-nav .open .dropdown-menu{position:static;float:none;width:auto;margin-top:0;background-color:transparent;border:0;box-shadow:none}.navbar-nav .open .dropdown-menu .dropdown-header,.navbar-nav .open .dropdown-menu>li>a{padding:5px 15px 5px 25px}.navbar-nav .open .dropdown-menu>li>a{line-height:18px}.navbar-nav .open .dropdown-menu>li>a:focus,.navbar-nav .open .dropdown-menu>li>a:hover{background-image:none}}@media (min-width:541px){.navbar-nav{float:left;margin:0}.navbar-nav>li{float:left}.navbar-nav>li>a{padding-top:6px;padding-bottom:6px}}.navbar-form{padding:10px 0;border-top:1px solid transparent;border-bottom:1px solid transparent;-webkit-box-shadow:inset 0 1px 0 rgba(255,255,255,.1),0 1px 0 rgba(255,255,255,.1);box-shadow:inset 0 1px 0 rgba(255,255,255,.1),0 1px 0 rgba(255,255,255,.1);margin:-1px 0}@media (min-width:768px){.navbar-form .form-group{display:inline-block;margin-bottom:0;vertical-align:middle}.navbar-form .form-control{display:inline-block;width:auto;vertical-align:middle}.navbar-form .form-control-static{display:inline-block}.navbar-form .input-group{display:inline-table;vertical-align:middle}.navbar-form .input-group .form-control,.navbar-form .input-group .input-group-addon,.navbar-form .input-group .input-group-btn{width:auto}.navbar-form .input-group>.form-control{width:100%}.navbar-form .control-label{margin-bottom:0;vertical-align:middle}.navbar-form .checkbox,.navbar-form .radio{display:inline-block;margin-top:0;margin-bottom:0;vertical-align:middle}.navbar-form .checkbox label,.navbar-form .radio label{padding-left:0}.navbar-form .checkbox input[type=checkbox],.navbar-form .radio input[type=radio]{position:relative;margin-left:0}.navbar-form .has-feedback .form-control-feedback{top:0}}@media (max-width:540px){.navbar-form .form-group{margin-bottom:5px}.navbar-form .form-group:last-child{margin-bottom:0}}.navbar-nav>li>.dropdown-menu{margin-top:0;border-top-right-radius:0;border-top-left-radius:0}.navbar-fixed-bottom .navbar-nav>li>.dropdown-menu{margin-bottom:0;border-radius:2px 2px 0 0}.navbar-btn{margin-top:-1px;margin-bottom:-1px}.navbar-btn.btn-sm{margin-top:0;margin-bottom:0}.navbar-btn.btn-xs{margin-top:4px;margin-bottom:4px}.navbar-text{margin-top:6px;margin-bottom:6px}@media (min-width:541px){.navbar-form{width:auto;border:0;margin-left:0;margin-right:0;padding-top:0;padding-bottom:0;-webkit-box-shadow:none;box-shadow:none}.navbar-text{float:left;margin-left:0;margin-right:0}.navbar-left{float:left!important;float:left}.navbar-right{float:right!important;float:right;margin-right:0}.navbar-right~.navbar-right{margin-right:0}}.navbar-default{background-color:#f8f8f8;border-color:#e7e7e7}.navbar-default .navbar-brand{color:#777}.navbar-default .navbar-brand:focus,.navbar-default .navbar-brand:hover{color:#5e5e5e;background-color:transparent}.navbar-default .navbar-nav>li>a,.navbar-default .navbar-text{color:#777}.navbar-default .navbar-nav>li>a:focus,.navbar-default .navbar-nav>li>a:hover{color:#333;background-color:transparent}.navbar-default .navbar-nav>.active>a,.navbar-default .navbar-nav>.active>a:focus,.navbar-default .navbar-nav>.active>a:hover{color:#555;background-color:#e7e7e7}.navbar-default .navbar-nav>.disabled>a,.navbar-default .navbar-nav>.disabled>a:focus,.navbar-default .navbar-nav>.disabled>a:hover{color:#ccc;background-color:transparent}.navbar-default .navbar-toggle{border-color:#ddd}.navbar-default .navbar-toggle:focus,.navbar-default .navbar-toggle:hover{background-color:#ddd}.navbar-default .navbar-toggle .icon-bar{background-color:#888}.navbar-default .navbar-collapse,.navbar-default .navbar-form{border-color:#e7e7e7}.navbar-default .navbar-nav>.open>a,.navbar-default .navbar-nav>.open>a:focus,.navbar-default .navbar-nav>.open>a:hover{background-color:#e7e7e7;color:#555}@media (max-width:540px){.navbar-default .navbar-nav .open .dropdown-menu>li>a{color:#777}.navbar-default .navbar-nav .open .dropdown-menu>li>a:focus,.navbar-default .navbar-nav .open .dropdown-menu>li>a:hover{color:#333;background-color:transparent}.navbar-default .navbar-nav .open .dropdown-menu>.active>a,.navbar-default .navbar-nav .open .dropdown-menu>.active>a:focus,.navbar-default .navbar-nav .open .dropdown-menu>.active>a:hover{color:#555;background-color:#e7e7e7}.navbar-default .navbar-nav .open .dropdown-menu>.disabled>a,.navbar-default .navbar-nav .open .dropdown-menu>.disabled>a:focus,.navbar-default .navbar-nav .open .dropdown-menu>.disabled>a:hover{color:#ccc;background-color:transparent}}.navbar-default .navbar-link{color:#777}.navbar-default .navbar-link:hover{color:#333}.navbar-default .btn-link{color:#777}.navbar-default .btn-link:focus,.navbar-default .btn-link:hover{color:#333}.navbar-default .btn-link[disabled]:focus,.navbar-default .btn-link[disabled]:hover,fieldset[disabled] .navbar-default .btn-link:focus,fieldset[disabled] .navbar-default .btn-link:hover{color:#ccc}.navbar-inverse{background-color:#222;border-color:#080808}.navbar-inverse .navbar-brand{color:#9d9d9d}.navbar-inverse .navbar-brand:focus,.navbar-inverse .navbar-brand:hover{color:#fff;background-color:transparent}.navbar-inverse .navbar-nav>li>a,.navbar-inverse .navbar-text{color:#9d9d9d}.navbar-inverse .navbar-nav>li>a:focus,.navbar-inverse .navbar-nav>li>a:hover{color:#fff;background-color:transparent}.navbar-inverse .navbar-nav>.active>a,.navbar-inverse .navbar-nav>.active>a:focus,.navbar-inverse .navbar-nav>.active>a:hover{color:#fff;background-color:#080808}.navbar-inverse .navbar-nav>.disabled>a,.navbar-inverse .navbar-nav>.disabled>a:focus,.navbar-inverse .navbar-nav>.disabled>a:hover{color:#444;background-color:transparent}.navbar-inverse .navbar-toggle{border-color:#333}.navbar-inverse .navbar-toggle:focus,.navbar-inverse .navbar-toggle:hover{background-color:#333}.navbar-inverse .navbar-toggle .icon-bar{background-color:#fff}.navbar-inverse .navbar-collapse,.navbar-inverse .navbar-form{border-color:#101010}.navbar-inverse .navbar-nav>.open>a,.navbar-inverse .navbar-nav>.open>a:focus,.navbar-inverse .navbar-nav>.open>a:hover{background-color:#080808;color:#fff}@media (max-width:540px){.navbar-inverse .navbar-nav .open .dropdown-menu>.dropdown-header{border-color:#080808}.navbar-inverse .navbar-nav .open .dropdown-menu .divider{background-color:#080808}.navbar-inverse .navbar-nav .open .dropdown-menu>li>a{color:#9d9d9d}.navbar-inverse .navbar-nav .open .dropdown-menu>li>a:focus,.navbar-inverse .navbar-nav .open .dropdown-menu>li>a:hover{color:#fff;background-color:transparent}.navbar-inverse .navbar-nav .open .dropdown-menu>.active>a,.navbar-inverse .navbar-nav .open .dropdown-menu>.active>a:focus,.navbar-inverse .navbar-nav .open .dropdown-menu>.active>a:hover{color:#fff;background-color:#080808}.navbar-inverse .navbar-nav .open .dropdown-menu>.disabled>a,.navbar-inverse .navbar-nav .open .dropdown-menu>.disabled>a:focus,.navbar-inverse .navbar-nav .open .dropdown-menu>.disabled>a:hover{color:#444;background-color:transparent}}.navbar-inverse .navbar-link{color:#9d9d9d}.navbar-inverse .navbar-link:hover{color:#fff}.navbar-inverse .btn-link{color:#9d9d9d}.navbar-inverse .btn-link:focus,.navbar-inverse .btn-link:hover{color:#fff}.navbar-inverse .btn-link[disabled]:focus,.navbar-inverse .btn-link[disabled]:hover,fieldset[disabled] .navbar-inverse .btn-link:focus,fieldset[disabled] .navbar-inverse .btn-link:hover{color:#444}.breadcrumb{padding:8px 15px;margin-bottom:18px;list-style:none;background-color:#f5f5f5;border-radius:2px}.breadcrumb>li{display:inline-block}.breadcrumb>li+li:before{content:"/\00a0";padding:0 5px;color:#5e5e5e}.breadcrumb>.active{color:#777}.pagination{display:inline-block;padding-left:0;margin:18px 0;border-radius:2px}.pagination>li{display:inline}.pagination>li>a,.pagination>li>span{position:relative;float:left;padding:6px 12px;line-height:1.42857143;text-decoration:none;color:#337ab7;background-color:#fff;border:1px solid #ddd;margin-left:-1px}.pagination>li:first-child>a,.pagination>li:first-child>span{margin-left:0;border-bottom-left-radius:2px;border-top-left-radius:2px}.pagination>li:last-child>a,.pagination>li:last-child>span{border-bottom-right-radius:2px;border-top-right-radius:2px}.pagination>li>a:focus,.pagination>li>a:hover,.pagination>li>span:focus,.pagination>li>span:hover{color:#23527c;background-color:#eee;border-color:#ddd}.pagination>.active>a,.pagination>.active>a:focus,.pagination>.active>a:hover,.pagination>.active>span,.pagination>.active>span:focus,.pagination>.active>span:hover{z-index:2;color:#fff;background-color:#337ab7;border-color:#337ab7;cursor:default}.pagination>.disabled>a,.pagination>.disabled>a:focus,.pagination>.disabled>a:hover,.pagination>.disabled>span,.pagination>.disabled>span:focus,.pagination>.disabled>span:hover{color:#777;background-color:#fff;border-color:#ddd;cursor:not-allowed}.pagination-lg>li>a,.pagination-lg>li>span{padding:10px 16px;font-size:17px}.pagination-lg>li:first-child>a,.pagination-lg>li:first-child>span{border-bottom-left-radius:3px;border-top-left-radius:3px}.pagination-lg>li:last-child>a,.pagination-lg>li:last-child>span{border-bottom-right-radius:3px;border-top-right-radius:3px}.pagination-sm>li>a,.pagination-sm>li>span{padding:5px 10px;font-size:12px}.pagination-sm>li:first-child>a,.pagination-sm>li:first-child>span{border-bottom-left-radius:1px;border-top-left-radius:1px}.pagination-sm>li:last-child>a,.pagination-sm>li:last-child>span{border-bottom-right-radius:1px;border-top-right-radius:1px}.pager{padding-left:0;margin:18px 0;list-style:none;text-align:center}.pager li{display:inline}.pager li>a,.pager li>span{display:inline-block;padding:5px 14px;background-color:#fff;border:1px solid #ddd;border-radius:15px}.pager li>a:focus,.pager li>a:hover{text-decoration:none;background-color:#eee}.pager .next>a,.pager .next>span{float:right}.pager .previous>a,.pager .previous>span{float:left}.pager .disabled>a,.pager .disabled>a:focus,.pager .disabled>a:hover,.pager .disabled>span{color:#777;background-color:#fff;cursor:not-allowed}.label{display:inline;padding:.2em .6em .3em;font-size:75%;font-weight:700;line-height:1;color:#fff;text-align:center;white-space:nowrap;vertical-align:baseline;border-radius:.25em}a.label:focus,a.label:hover{color:#fff;text-decoration:none;cursor:pointer}.label:empty{display:none}.btn .label{position:relative;top:-1px}.label-default{background-color:#777}.label-default[href]:focus,.label-default[href]:hover{background-color:#5e5e5e}.label-primary{background-color:#337ab7}.label-primary[href]:focus,.label-primary[href]:hover{background-color:#286090}.label-success{background-color:#5cb85c}.label-success[href]:focus,.label-success[href]:hover{background-color:#449d44}.label-info{background-color:#5bc0de}.label-info[href]:focus,.label-info[href]:hover{background-color:#31b0d5}.label-warning{background-color:#f0ad4e}.label-warning[href]:focus,.label-warning[href]:hover{background-color:#ec971f}.label-danger{background-color:#d9534f}.label-danger[href]:focus,.label-danger[href]:hover{background-color:#c9302c}.badge{display:inline-block;min-width:10px;padding:3px 7px;font-size:12px;font-weight:700;color:#fff;line-height:1;vertical-align:baseline;white-space:nowrap;text-align:center;background-color:#777;border-radius:10px}.badge:empty{display:none}.btn .badge{position:relative;top:-1px}.btn-group-xs>.btn .badge,.btn-xs .badge{top:0;padding:1px 5px}a.badge:focus,a.badge:hover{color:#fff;text-decoration:none;cursor:pointer}.list-group-item.active>.badge,.nav-pills>.active>a>.badge{color:#337ab7;background-color:#fff}.list-group-item>.badge{float:right}.list-group-item>.badge+.badge{margin-right:5px}.nav-pills>li>a>.badge{margin-left:3px}.jumbotron{padding:30px 15px;margin-bottom:30px;color:inherit;background-color:#eee}.jumbotron .h1,.jumbotron h1{color:inherit}.jumbotron p{margin-bottom:15px;font-size:20px;font-weight:200}.jumbotron>hr{border-top-color:#d5d5d5}.container .jumbotron,.container-fluid .jumbotron{border-radius:3px}.jumbotron .container{max-width:100%}@media screen and (min-width:768px){.jumbotron{padding:48px 0}.container .jumbotron,.container-fluid .jumbotron{padding-left:60px;padding-right:60px}.jumbotron .h1,.jumbotron h1{font-size:58.5px}}.thumbnail{display:block;padding:4px;margin-bottom:18px;line-height:1.42857143;background-color:#fff;border:1px solid #ddd;border-radius:2px;-webkit-transition:border .2s ease-in-out;-o-transition:border .2s ease-in-out;transition:border .2s ease-in-out}.thumbnail a>img,.thumbnail>img{margin-left:auto;margin-right:auto}a.thumbnail.active,a.thumbnail:focus,a.thumbnail:hover{border-color:#337ab7}.thumbnail .caption{padding:9px;color:#000}.alert{padding:15px;margin-bottom:18px;border:1px solid transparent;border-radius:2px}.alert h4{margin-top:0;color:inherit}.alert .alert-link{font-weight:700}.alert>p,.alert>ul{margin-bottom:0}.alert>p+p{margin-top:5px}.alert-dismissable,.alert-dismissible{padding-right:35px}.alert-dismissable .close,.alert-dismissible .close{position:relative;top:-2px;right:-21px;color:inherit}.alert-success{background-color:#dff0d8;border-color:#d6e9c6;color:#3c763d}.alert-success hr{border-top-color:#c9e2b3}.alert-success .alert-link{color:#2b542c}.alert-info{background-color:#d9edf7;border-color:#bce8f1;color:#31708f}.alert-info hr{border-top-color:#a6e1ec}.alert-info .alert-link{color:#245269}.alert-warning{background-color:#fcf8e3;border-color:#faebcc;color:#8a6d3b}.alert-warning hr{border-top-color:#f7e1b5}.alert-warning .alert-link{color:#66512c}.alert-danger{background-color:#f2dede;border-color:#ebccd1;color:#a94442}.alert-danger hr{border-top-color:#e4b9c0}.alert-danger .alert-link{color:#843534}@-webkit-keyframes progress-bar-stripes{from{background-position:40px 0}to{background-position:0 0}}@keyframes progress-bar-stripes{from{background-position:40px 0}to{background-position:0 0}}.progress{overflow:hidden;height:18px;margin-bottom:18px;background-color:#f5f5f5;border-radius:2px;-webkit-box-shadow:inset 0 1px 2px rgba(0,0,0,.1);box-shadow:inset 0 1px 2px rgba(0,0,0,.1)}.progress-bar{float:left;width:0;height:100%;font-size:12px;line-height:18px;color:#fff;text-align:center;background-color:#337ab7;-webkit-box-shadow:inset 0 -1px 0 rgba(0,0,0,.15);box-shadow:inset 0 -1px 0 rgba(0,0,0,.15);-webkit-transition:width .6s ease;-o-transition:width .6s ease;transition:width .6s ease}.progress-bar-striped,.progress-striped .progress-bar{background-image:-webkit-linear-gradient(45deg,rgba(255,255,255,.15) 25%,transparent 25%,transparent 50%,rgba(255,255,255,.15) 50%,rgba(255,255,255,.15) 75%,transparent 75%,transparent);background-image:-o-linear-gradient(45deg,rgba(255,255,255,.15) 25%,transparent 25%,transparent 50%,rgba(255,255,255,.15) 50%,rgba(255,255,255,.15) 75%,transparent 75%,transparent);background-image:linear-gradient(45deg,rgba(255,255,255,.15) 25%,transparent 25%,transparent 50%,rgba(255,255,255,.15) 50%,rgba(255,255,255,.15) 75%,transparent 75%,transparent);background-size:40px 40px}.progress-bar.active,.progress.active .progress-bar{-webkit-animation:progress-bar-stripes 2s linear infinite;-o-animation:progress-bar-stripes 2s linear infinite;animation:progress-bar-stripes 2s linear infinite}.progress-bar-success{background-color:#5cb85c}.progress-striped .progress-bar-success{background-image:-webkit-linear-gradient(45deg,rgba(255,255,255,.15) 25%,transparent 25%,transparent 50%,rgba(255,255,255,.15) 50%,rgba(255,255,255,.15) 75%,transparent 75%,transparent);background-image:-o-linear-gradient(45deg,rgba(255,255,255,.15) 25%,transparent 25%,transparent 50%,rgba(255,255,255,.15) 50%,rgba(255,255,255,.15) 75%,transparent 75%,transparent);background-image:linear-gradient(45deg,rgba(255,255,255,.15) 25%,transparent 25%,transparent 50%,rgba(255,255,255,.15) 50%,rgba(255,255,255,.15) 75%,transparent 75%,transparent)}.progress-bar-info{background-color:#5bc0de}.progress-striped .progress-bar-info{background-image:-webkit-linear-gradient(45deg,rgba(255,255,255,.15) 25%,transparent 25%,transparent 50%,rgba(255,255,255,.15) 50%,rgba(255,255,255,.15) 75%,transparent 75%,transparent);background-image:-o-linear-gradient(45deg,rgba(255,255,255,.15) 25%,transparent 25%,transparent 50%,rgba(255,255,255,.15) 50%,rgba(255,255,255,.15) 75%,transparent 75%,transparent);background-image:linear-gradient(45deg,rgba(255,255,255,.15) 25%,transparent 25%,transparent 50%,rgba(255,255,255,.15) 50%,rgba(255,255,255,.15) 75%,transparent 75%,transparent)}.progress-bar-warning{background-color:#f0ad4e}.progress-striped .progress-bar-warning{background-image:-webkit-linear-gradient(45deg,rgba(255,255,255,.15) 25%,transparent 25%,transparent 50%,rgba(255,255,255,.15) 50%,rgba(255,255,255,.15) 75%,transparent 75%,transparent);background-image:-o-linear-gradient(45deg,rgba(255,255,255,.15) 25%,transparent 25%,transparent 50%,rgba(255,255,255,.15) 50%,rgba(255,255,255,.15) 75%,transparent 75%,transparent);background-image:linear-gradient(45deg,rgba(255,255,255,.15) 25%,transparent 25%,transparent 50%,rgba(255,255,255,.15) 50%,rgba(255,255,255,.15) 75%,transparent 75%,transparent)}.progress-bar-danger{background-color:#d9534f}.progress-striped .progress-bar-danger{background-image:-webkit-linear-gradient(45deg,rgba(255,255,255,.15) 25%,transparent 25%,transparent 50%,rgba(255,255,255,.15) 50%,rgba(255,255,255,.15) 75%,transparent 75%,transparent);background-image:-o-linear-gradient(45deg,rgba(255,255,255,.15) 25%,transparent 25%,transparent 50%,rgba(255,255,255,.15) 50%,rgba(255,255,255,.15) 75%,transparent 75%,transparent);background-image:linear-gradient(45deg,rgba(255,255,255,.15) 25%,transparent 25%,transparent 50%,rgba(255,255,255,.15) 50%,rgba(255,255,255,.15) 75%,transparent 75%,transparent)}.media{margin-top:15px}.media:first-child{margin-top:0}.media,.media-body{zoom:1;overflow:hidden}.media-body{width:10000px}.media-object{display:block}.media-right,.media>.pull-right{padding-left:10px}.media-left,.media>.pull-left{padding-right:10px}.media-body,.media-left,.media-right{display:table-cell;vertical-align:top}.media-middle{vertical-align:middle}.media-bottom{vertical-align:bottom}.media-heading{margin-top:0;margin-bottom:5px}.media-list{padding-left:0;list-style:none}.list-group{margin-bottom:20px;padding-left:0}.list-group-item{position:relative;display:block;padding:10px 15px;margin-bottom:-1px;background-color:#fff;border:1px solid #ddd}.list-group-item:first-child{border-top-right-radius:2px;border-top-left-radius:2px}.list-group-item:last-child{margin-bottom:0;border-bottom-right-radius:2px;border-bottom-left-radius:2px}a.list-group-item{color:#555}a.list-group-item .list-group-item-heading{color:#333}a.list-group-item:focus,a.list-group-item:hover{text-decoration:none;color:#555;background-color:#f5f5f5}.list-group-item.disabled,.list-group-item.disabled:focus,.list-group-item.disabled:hover{background-color:#eee;color:#777;cursor:not-allowed}.list-group-item.disabled .list-group-item-heading,.list-group-item.disabled:focus .list-group-item-heading,.list-group-item.disabled:hover .list-group-item-heading{color:inherit}.list-group-item.disabled .list-group-item-text,.list-group-item.disabled:focus .list-group-item-text,.list-group-item.disabled:hover .list-group-item-text{color:#777}.list-group-item.active,.list-group-item.active:focus,.list-group-item.active:hover{z-index:2;color:#fff;background-color:#337ab7;border-color:#337ab7}.list-group-item.active .list-group-item-heading,.list-group-item.active .list-group-item-heading>.small,.list-group-item.active .list-group-item-heading>small,.list-group-item.active:focus .list-group-item-heading,.list-group-item.active:focus .list-group-item-heading>.small,.list-group-item.active:focus .list-group-item-heading>small,.list-group-item.active:hover .list-group-item-heading,.list-group-item.active:hover .list-group-item-heading>.small,.list-group-item.active:hover .list-group-item-heading>small{color:inherit}.list-group-item.active .list-group-item-text,.list-group-item.active:focus .list-group-item-text,.list-group-item.active:hover .list-group-item-text{color:#c7ddef}.list-group-item-success{color:#3c763d;background-color:#dff0d8}a.list-group-item-success{color:#3c763d}a.list-group-item-success .list-group-item-heading{color:inherit}a.list-group-item-success:focus,a.list-group-item-success:hover{color:#3c763d;background-color:#d0e9c6}a.list-group-item-success.active,a.list-group-item-success.active:focus,a.list-group-item-success.active:hover{color:#fff;background-color:#3c763d;border-color:#3c763d}.list-group-item-info{color:#31708f;background-color:#d9edf7}a.list-group-item-info{color:#31708f}a.list-group-item-info .list-group-item-heading{color:inherit}a.list-group-item-info:focus,a.list-group-item-info:hover{color:#31708f;background-color:#c4e3f3}a.list-group-item-info.active,a.list-group-item-info.active:focus,a.list-group-item-info.active:hover{color:#fff;background-color:#31708f;border-color:#31708f}.list-group-item-warning{color:#8a6d3b;background-color:#fcf8e3}a.list-group-item-warning{color:#8a6d3b}a.list-group-item-warning .list-group-item-heading{color:inherit}a.list-group-item-warning:focus,a.list-group-item-warning:hover{color:#8a6d3b;background-color:#faf2cc}a.list-group-item-warning.active,a.list-group-item-warning.active:focus,a.list-group-item-warning.active:hover{color:#fff;background-color:#8a6d3b;border-color:#8a6d3b}.list-group-item-danger{color:#a94442;background-color:#f2dede}a.list-group-item-danger{color:#a94442}a.list-group-item-danger .list-group-item-heading{color:inherit}a.list-group-item-danger:focus,a.list-group-item-danger:hover{color:#a94442;background-color:#ebcccc}a.list-group-item-danger.active,a.list-group-item-danger.active:focus,a.list-group-item-danger.active:hover{color:#fff;background-color:#a94442;border-color:#a94442}.list-group-item-heading{margin-top:0;margin-bottom:5px}.list-group-item-text{margin-bottom:0;line-height:1.3}.panel{margin-bottom:18px;background-color:#fff;border:1px solid transparent;border-radius:2px;-webkit-box-shadow:0 1px 1px rgba(0,0,0,.05);box-shadow:0 1px 1px rgba(0,0,0,.05)}.panel-body{padding:15px}.panel-heading{padding:10px 15px;border-bottom:1px solid transparent;border-top-right-radius:1px;border-top-left-radius:1px}.panel-heading>.dropdown .dropdown-toggle{color:inherit}.panel-title{margin-top:0;margin-bottom:0;font-size:15px;color:inherit}.panel-title>.small,.panel-title>.small>a,.panel-title>a,.panel-title>small,.panel-title>small>a{color:inherit}.panel-footer{padding:10px 15px;background-color:#f5f5f5;border-top:1px solid #ddd;border-bottom-right-radius:1px;border-bottom-left-radius:1px}.panel>.list-group,.panel>.panel-collapse>.list-group{margin-bottom:0}.panel>.list-group .list-group-item,.panel>.panel-collapse>.list-group .list-group-item{border-width:1px 0;border-radius:0}.panel>.list-group:first-child .list-group-item:first-child,.panel>.panel-collapse>.list-group:first-child .list-group-item:first-child{border-top:0;border-top-right-radius:1px;border-top-left-radius:1px}.panel>.list-group:last-child .list-group-item:last-child,.panel>.panel-collapse>.list-group:last-child .list-group-item:last-child{border-bottom:0;border-bottom-right-radius:1px;border-bottom-left-radius:1px}.list-group+.panel-footer,.panel-heading+.list-group .list-group-item:first-child{border-top-width:0}.panel>.panel-collapse>.table,.panel>.table,.panel>.table-responsive>.table{margin-bottom:0}.panel>.panel-collapse>.table caption,.panel>.table caption,.panel>.table-responsive>.table caption{padding-left:15px;padding-right:15px}.panel>.table-responsive:first-child>.table:first-child,.panel>.table:first-child{border-top-right-radius:1px;border-top-left-radius:1px}.panel>.table-responsive:first-child>.table:first-child>tbody:first-child>tr:first-child,.panel>.table-responsive:first-child>.table:first-child>thead:first-child>tr:first-child,.panel>.table:first-child>tbody:first-child>tr:first-child,.panel>.table:first-child>thead:first-child>tr:first-child{border-top-left-radius:1px;border-top-right-radius:1px}.panel>.table-responsive:first-child>.table:first-child>tbody:first-child>tr:first-child td:first-child,.panel>.table-responsive:first-child>.table:first-child>tbody:first-child>tr:first-child th:first-child,.panel>.table-responsive:first-child>.table:first-child>thead:first-child>tr:first-child td:first-child,.panel>.table-responsive:first-child>.table:first-child>thead:first-child>tr:first-child th:first-child,.panel>.table:first-child>tbody:first-child>tr:first-child td:first-child,.panel>.table:first-child>tbody:first-child>tr:first-child th:first-child,.panel>.table:first-child>thead:first-child>tr:first-child td:first-child,.panel>.table:first-child>thead:first-child>tr:first-child th:first-child{border-top-left-radius:1px}.panel>.table-responsive:first-child>.table:first-child>tbody:first-child>tr:first-child td:last-child,.panel>.table-responsive:first-child>.table:first-child>tbody:first-child>tr:first-child th:last-child,.panel>.table-responsive:first-child>.table:first-child>thead:first-child>tr:first-child td:last-child,.panel>.table-responsive:first-child>.table:first-child>thead:first-child>tr:first-child th:last-child,.panel>.table:first-child>tbody:first-child>tr:first-child td:last-child,.panel>.table:first-child>tbody:first-child>tr:first-child th:last-child,.panel>.table:first-child>thead:first-child>tr:first-child td:last-child,.panel>.table:first-child>thead:first-child>tr:first-child th:last-child{border-top-right-radius:1px}.panel>.table-responsive:last-child>.table:last-child,.panel>.table:last-child{border-bottom-right-radius:1px;border-bottom-left-radius:1px}.panel>.table-responsive:last-child>.table:last-child>tbody:last-child>tr:last-child,.panel>.table-responsive:last-child>.table:last-child>tfoot:last-child>tr:last-child,.panel>.table:last-child>tbody:last-child>tr:last-child,.panel>.table:last-child>tfoot:last-child>tr:last-child{border-bottom-left-radius:1px;border-bottom-right-radius:1px}.panel>.table-responsive:last-child>.table:last-child>tbody:last-child>tr:last-child td:first-child,.panel>.table-responsive:last-child>.table:last-child>tbody:last-child>tr:last-child th:first-child,.panel>.table-responsive:last-child>.table:last-child>tfoot:last-child>tr:last-child td:first-child,.panel>.table-responsive:last-child>.table:last-child>tfoot:last-child>tr:last-child th:first-child,.panel>.table:last-child>tbody:last-child>tr:last-child td:first-child,.panel>.table:last-child>tbody:last-child>tr:last-child th:first-child,.panel>.table:last-child>tfoot:last-child>tr:last-child td:first-child,.panel>.table:last-child>tfoot:last-child>tr:last-child th:first-child{border-bottom-left-radius:1px}.panel>.table-responsive:last-child>.table:last-child>tbody:last-child>tr:last-child td:last-child,.panel>.table-responsive:last-child>.table:last-child>tbody:last-child>tr:last-child th:last-child,.panel>.table-responsive:last-child>.table:last-child>tfoot:last-child>tr:last-child td:last-child,.panel>.table-responsive:last-child>.table:last-child>tfoot:last-child>tr:last-child th:last-child,.panel>.table:last-child>tbody:last-child>tr:last-child td:last-child,.panel>.table:last-child>tbody:last-child>tr:last-child th:last-child,.panel>.table:last-child>tfoot:last-child>tr:last-child td:last-child,.panel>.table:last-child>tfoot:last-child>tr:last-child th:last-child{border-bottom-right-radius:1px}.panel>.panel-body+.table,.panel>.panel-body+.table-responsive,.panel>.table+.panel-body,.panel>.table-responsive+.panel-body{border-top:1px solid #ddd}.panel>.table>tbody:first-child>tr:first-child td,.panel>.table>tbody:first-child>tr:first-child th{border-top:0}.panel>.table-bordered,.panel>.table-responsive>.table-bordered{border:0}.panel>.table-bordered>tbody>tr>td:first-child,.panel>.table-bordered>tbody>tr>th:first-child,.panel>.table-bordered>tfoot>tr>td:first-child,.panel>.table-bordered>tfoot>tr>th:first-child,.panel>.table-bordered>thead>tr>td:first-child,.panel>.table-bordered>thead>tr>th:first-child,.panel>.table-responsive>.table-bordered>tbody>tr>td:first-child,.panel>.table-responsive>.table-bordered>tbody>tr>th:first-child,.panel>.table-responsive>.table-bordered>tfoot>tr>td:first-child,.panel>.table-responsive>.table-bordered>tfoot>tr>th:first-child,.panel>.table-responsive>.table-bordered>thead>tr>td:first-child,.panel>.table-responsive>.table-bordered>thead>tr>th:first-child{border-left:0}.panel>.table-bordered>tbody>tr>td:last-child,.panel>.table-bordered>tbody>tr>th:last-child,.panel>.table-bordered>tfoot>tr>td:last-child,.panel>.table-bordered>tfoot>tr>th:last-child,.panel>.table-bordered>thead>tr>td:last-child,.panel>.table-bordered>thead>tr>th:last-child,.panel>.table-responsive>.table-bordered>tbody>tr>td:last-child,.panel>.table-responsive>.table-bordered>tbody>tr>th:last-child,.panel>.table-responsive>.table-bordered>tfoot>tr>td:last-child,.panel>.table-responsive>.table-bordered>tfoot>tr>th:last-child,.panel>.table-responsive>.table-bordered>thead>tr>td:last-child,.panel>.table-responsive>.table-bordered>thead>tr>th:last-child{border-right:0}.panel>.table-bordered>tbody>tr:first-child>td,.panel>.table-bordered>tbody>tr:first-child>th,.panel>.table-bordered>tbody>tr:last-child>td,.panel>.table-bordered>tbody>tr:last-child>th,.panel>.table-bordered>tfoot>tr:last-child>td,.panel>.table-bordered>tfoot>tr:last-child>th,.panel>.table-bordered>thead>tr:first-child>td,.panel>.table-bordered>thead>tr:first-child>th,.panel>.table-responsive>.table-bordered>tbody>tr:first-child>td,.panel>.table-responsive>.table-bordered>tbody>tr:first-child>th,.panel>.table-responsive>.table-bordered>tbody>tr:last-child>td,.panel>.table-responsive>.table-bordered>tbody>tr:last-child>th,.panel>.table-responsive>.table-bordered>tfoot>tr:last-child>td,.panel>.table-responsive>.table-bordered>tfoot>tr:last-child>th,.panel>.table-responsive>.table-bordered>thead>tr:first-child>td,.panel>.table-responsive>.table-bordered>thead>tr:first-child>th{border-bottom:0}.panel>.table-responsive{border:0;margin-bottom:0}.panel-group{margin-bottom:18px}.panel-group .panel{margin-bottom:0;border-radius:2px}.panel-group .panel+.panel{margin-top:5px}.panel-group .panel-heading{border-bottom:0}.panel-group .panel-heading+.panel-collapse>.list-group,.panel-group .panel-heading+.panel-collapse>.panel-body{border-top:1px solid #ddd}.panel-group .panel-footer{border-top:0}.panel-group .panel-footer+.panel-collapse .panel-body{border-bottom:1px solid #ddd}.panel-default{border-color:#ddd}.panel-default>.panel-heading{color:#333;background-color:#f5f5f5;border-color:#ddd}.panel-default>.panel-heading+.panel-collapse>.panel-body{border-top-color:#ddd}.panel-default>.panel-heading .badge{color:#f5f5f5;background-color:#333}.panel-default>.panel-footer+.panel-collapse>.panel-body{border-bottom-color:#ddd}.panel-primary{border-color:#337ab7}.panel-primary>.panel-heading{color:#fff;background-color:#337ab7;border-color:#337ab7}.panel-primary>.panel-heading+.panel-collapse>.panel-body{border-top-color:#337ab7}.panel-primary>.panel-heading .badge{color:#337ab7;background-color:#fff}.panel-primary>.panel-footer+.panel-collapse>.panel-body{border-bottom-color:#337ab7}.panel-success{border-color:#d6e9c6}.panel-success>.panel-heading{color:#3c763d;background-color:#dff0d8;border-color:#d6e9c6}.panel-success>.panel-heading+.panel-collapse>.panel-body{border-top-color:#d6e9c6}.panel-success>.panel-heading .badge{color:#dff0d8;background-color:#3c763d}.panel-success>.panel-footer+.panel-collapse>.panel-body{border-bottom-color:#d6e9c6}.panel-info{border-color:#bce8f1}.panel-info>.panel-heading{color:#31708f;background-color:#d9edf7;border-color:#bce8f1}.panel-info>.panel-heading+.panel-collapse>.panel-body{border-top-color:#bce8f1}.panel-info>.panel-heading .badge{color:#d9edf7;background-color:#31708f}.panel-info>.panel-footer+.panel-collapse>.panel-body{border-bottom-color:#bce8f1}.panel-warning{border-color:#faebcc}.panel-warning>.panel-heading{color:#8a6d3b;background-color:#fcf8e3;border-color:#faebcc}.panel-warning>.panel-heading+.panel-collapse>.panel-body{border-top-color:#faebcc}.panel-warning>.panel-heading .badge{color:#fcf8e3;background-color:#8a6d3b}.panel-warning>.panel-footer+.panel-collapse>.panel-body{border-bottom-color:#faebcc}.panel-danger{border-color:#ebccd1}.panel-danger>.panel-heading{color:#a94442;background-color:#f2dede;border-color:#ebccd1}.panel-danger>.panel-heading+.panel-collapse>.panel-body{border-top-color:#ebccd1}.panel-danger>.panel-heading .badge{color:#f2dede;background-color:#a94442}.panel-danger>.panel-footer+.panel-collapse>.panel-body{border-bottom-color:#ebccd1}.embed-responsive{position:relative;display:block;height:0;padding:0;overflow:hidden}.embed-responsive .embed-responsive-item,.embed-responsive embed,.embed-responsive iframe,.embed-responsive object,.embed-responsive video{position:absolute;top:0;left:0;bottom:0;height:100%;width:100%;border:0}.embed-responsive-16by9{padding-bottom:56.25%}.embed-responsive-4by3{padding-bottom:75%}.well{min-height:20px;padding:19px;margin-bottom:20px;background-color:#f5f5f5;border:1px solid #e3e3e3;border-radius:2px;-webkit-box-shadow:inset 0 1px 1px rgba(0,0,0,.05);box-shadow:inset 0 1px 1px rgba(0,0,0,.05)}.well blockquote{border-color:#ddd;border-color:rgba(0,0,0,.15)}.well-lg{padding:24px;border-radius:3px}.well-sm{padding:9px;border-radius:1px}.close{float:right;font-size:19.5px;font-weight:700;line-height:1;color:#000;text-shadow:0 1px 0 #fff;opacity:.2;filter:alpha(opacity=20)}.close:focus,.close:hover{color:#000;text-decoration:none;cursor:pointer;opacity:.5;filter:alpha(opacity=50)}button.close{padding:0;cursor:pointer;background:0 0;border:0;-webkit-appearance:none}.modal-open{overflow:hidden}.modal{display:none;overflow:hidden;position:fixed;top:0;right:0;bottom:0;left:0;z-index:1050;-webkit-overflow-scrolling:touch;outline:0}.modal.fade .modal-dialog{-webkit-transition:-webkit-transform .3s ease-out;-moz-transition:-moz-transform .3s ease-out;-o-transition:-o-transform .3s ease-out;transition:transform .3s ease-out}.modal.in .modal-dialog{-webkit-transform:translate(0,0);-ms-transform:translate(0,0);-o-transform:translate(0,0);transform:translate(0,0)}.modal-open .modal{overflow-x:hidden;overflow-y:auto}.modal-dialog{position:relative;width:auto;margin:10px}.modal-content{position:relative;background-color:#fff;border:1px solid #999;border:1px solid rgba(0,0,0,.2);border-radius:3px;-webkit-box-shadow:0 3px 9px rgba(0,0,0,.5);box-shadow:0 3px 9px rgba(0,0,0,.5);background-clip:padding-box;outline:0}.modal-backdrop{position:fixed;top:0;right:0;bottom:0;left:0;z-index:1040;background-color:#000}.modal-backdrop.fade{opacity:0;filter:alpha(opacity=0)}.modal-backdrop.in{opacity:.5;filter:alpha(opacity=50)}.modal-header{padding:15px;border-bottom:1px solid #e5e5e5;min-height:16.43px}.modal-header .close{margin-top:-2px}.modal-title{margin:0;line-height:1.42857143}.modal-body{position:relative;padding:15px}.modal-footer{padding:15px;text-align:right;border-top:1px solid #e5e5e5}.modal-footer .btn+.btn{margin-left:5px;margin-bottom:0}.modal-footer .btn-group .btn+.btn{margin-left:-1px}.modal-footer .btn-block+.btn-block{margin-left:0}.modal-scrollbar-measure{position:absolute;top:-9999px;width:50px;height:50px;overflow:scroll}@media (min-width:768px){.modal-dialog{width:600px;margin:30px auto}.modal-content{-webkit-box-shadow:0 5px 15px rgba(0,0,0,.5);box-shadow:0 5px 15px rgba(0,0,0,.5)}.modal-sm{width:300px}}@media (min-width:992px){.modal-lg{width:900px}}.tooltip{position:absolute;z-index:1070;display:block;font-family:"Helvetica Neue",Helvetica,Arial,sans-serif;font-size:12px;font-weight:400;line-height:1.4;opacity:0;filter:alpha(opacity=0)}.tooltip.in{opacity:.9;filter:alpha(opacity=90)}.tooltip.top{margin-top:-3px;padding:5px 0}.tooltip.right{margin-left:3px;padding:0 5px}.tooltip.bottom{margin-top:3px;padding:5px 0}.tooltip.left{margin-left:-3px;padding:0 5px}.tooltip-inner{max-width:200px;padding:3px 8px;color:#fff;text-align:center;text-decoration:none;background-color:#000;border-radius:2px}.tooltip-arrow{position:absolute;width:0;height:0;border-color:transparent;border-style:solid}.tooltip.top .tooltip-arrow{bottom:0;left:50%;margin-left:-5px;border-width:5px 5px 0;border-top-color:#000}.tooltip.top-left .tooltip-arrow{bottom:0;right:5px;margin-bottom:-5px;border-width:5px 5px 0;border-top-color:#000}.tooltip.top-right .tooltip-arrow{bottom:0;left:5px;margin-bottom:-5px;border-width:5px 5px 0;border-top-color:#000}.tooltip.right .tooltip-arrow{top:50%;left:0;margin-top:-5px;border-width:5px 5px 5px 0;border-right-color:#000}.tooltip.left .tooltip-arrow{top:50%;right:0;margin-top:-5px;border-width:5px 0 5px 5px;border-left-color:#000}.tooltip.bottom .tooltip-arrow{top:0;left:50%;margin-left:-5px;border-width:0 5px 5px;border-bottom-color:#000}.tooltip.bottom-left .tooltip-arrow{top:0;right:5px;margin-top:-5px;border-width:0 5px 5px;border-bottom-color:#000}.tooltip.bottom-right .tooltip-arrow{top:0;left:5px;margin-top:-5px;border-width:0 5px 5px;border-bottom-color:#000}.popover{position:absolute;top:0;left:0;z-index:1060;display:none;max-width:276px;padding:1px;font-family:"Helvetica Neue",Helvetica,Arial,sans-serif;font-size:13px;font-weight:400;line-height:1.42857143;text-align:left;background-color:#fff;background-clip:padding-box;border:1px solid #ccc;border:1px solid rgba(0,0,0,.2);border-radius:3px;-webkit-box-shadow:0 5px 10px rgba(0,0,0,.2);box-shadow:0 5px 10px rgba(0,0,0,.2);white-space:normal}.popover.top{margin-top:-10px}.popover.right{margin-left:10px}.popover.bottom{margin-top:10px}.popover.left{margin-left:-10px}.popover-title{margin:0;padding:8px 14px;font-size:13px;background-color:#f7f7f7;border-bottom:1px solid #ebebeb;border-radius:2px 2px 0 0}.popover-content{padding:9px 14px}.popover>.arrow,.popover>.arrow:after{position:absolute;display:block;width:0;height:0;border-color:transparent;border-style:solid}.popover>.arrow{border-width:11px}.popover>.arrow:after{border-width:10px;content:""}.popover.top>.arrow{left:50%;margin-left:-11px;border-bottom-width:0;border-top-color:#999;border-top-color:rgba(0,0,0,.25);bottom:-11px}.popover.top>.arrow:after{content:" ";bottom:1px;margin-left:-10px;border-bottom-width:0;border-top-color:#fff}.popover.right>.arrow{top:50%;left:-11px;margin-top:-11px;border-left-width:0;border-right-color:#999;border-right-color:rgba(0,0,0,.25)}.popover.right>.arrow:after{content:" ";left:1px;bottom:-10px;border-left-width:0;border-right-color:#fff}.popover.bottom>.arrow{left:50%;margin-left:-11px;border-top-width:0;border-bottom-color:#999;border-bottom-color:rgba(0,0,0,.25);top:-11px}.popover.bottom>.arrow:after{content:" ";top:1px;margin-left:-10px;border-top-width:0;border-bottom-color:#fff}.popover.left>.arrow{top:50%;right:-11px;margin-top:-11px;border-right-width:0;border-left-color:#999;border-left-color:rgba(0,0,0,.25)}.popover.left>.arrow:after{content:" ";right:1px;border-right-width:0;border-left-color:#fff;bottom:-10px}.carousel{position:relative}.carousel-inner{position:relative;overflow:hidden;width:100%}.carousel-inner>.item{display:none;position:relative;-webkit-transition:.6s ease-in-out left;-o-transition:.6s ease-in-out left;transition:.6s ease-in-out left}.carousel-inner>.item>a>img,.carousel-inner>.item>img{line-height:1}@media all and (transform-3d),(-webkit-transform-3d){.carousel-inner>.item{-webkit-transition:-webkit-transform .6s ease-in-out;-moz-transition:-moz-transform .6s ease-in-out;-o-transition:-o-transform .6s ease-in-out;transition:transform .6s ease-in-out;-webkit-backface-visibility:hidden;-moz-backface-visibility:hidden;backface-visibility:hidden;-webkit-perspective:1000;-moz-perspective:1000;perspective:1000}.carousel-inner>.item.active.right,.carousel-inner>.item.next{-webkit-transform:translate3d(100%,0,0);transform:translate3d(100%,0,0);left:0}.carousel-inner>.item.active.left,.carousel-inner>.item.prev{-webkit-transform:translate3d(-100%,0,0);transform:translate3d(-100%,0,0);left:0}.carousel-inner>.item.active,.carousel-inner>.item.next.left,.carousel-inner>.item.prev.right{-webkit-transform:translate3d(0,0,0);transform:translate3d(0,0,0);left:0}}.carousel-inner>.active,.carousel-inner>.next,.carousel-inner>.prev{display:block}.carousel-inner>.active{left:0}.carousel-inner>.next,.carousel-inner>.prev{position:absolute;top:0;width:100%}.carousel-inner>.next{left:100%}.carousel-inner>.prev{left:-100%}.carousel-inner>.next.left,.carousel-inner>.prev.right{left:0}.carousel-inner>.active.left{left:-100%}.carousel-inner>.active.right{left:100%}.carousel-control{position:absolute;top:0;left:0;bottom:0;width:15%;opacity:.5;filter:alpha(opacity=50);font-size:20px;color:#fff;text-align:center;text-shadow:0 1px 2px rgba(0,0,0,.6)}.carousel-control.left{background-image:-webkit-linear-gradient(left,rgba(0,0,0,.5) 0,rgba(0,0,0,.0001) 100%);background-image:-o-linear-gradient(left,rgba(0,0,0,.5) 0,rgba(0,0,0,.0001) 100%);background-image:linear-gradient(to right,rgba(0,0,0,.5) 0,rgba(0,0,0,.0001) 100%);background-repeat:repeat-x;filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#80000000', endColorstr='#00000000', GradientType=1)}.carousel-control.right{left:auto;right:0;background-image:-webkit-linear-gradient(left,rgba(0,0,0,.0001) 0,rgba(0,0,0,.5) 100%);background-image:-o-linear-gradient(left,rgba(0,0,0,.0001) 0,rgba(0,0,0,.5) 100%);background-image:linear-gradient(to right,rgba(0,0,0,.0001) 0,rgba(0,0,0,.5) 100%);background-repeat:repeat-x;filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#00000000', endColorstr='#80000000', GradientType=1)}.carousel-control:focus,.carousel-control:hover{outline:0;color:#fff;text-decoration:none;opacity:.9;filter:alpha(opacity=90)}.carousel-control .glyphicon-chevron-left,.carousel-control .glyphicon-chevron-right,.carousel-control .icon-next,.carousel-control .icon-prev{position:absolute;top:50%;z-index:5;display:inline-block}.carousel-control .glyphicon-chevron-left,.carousel-control .icon-prev{left:50%;margin-left:-10px}.carousel-control .glyphicon-chevron-right,.carousel-control .icon-next{right:50%;margin-right:-10px}.carousel-control .icon-next,.carousel-control .icon-prev{width:20px;height:20px;margin-top:-10px;line-height:1;font-family:serif}.carousel-control .icon-prev:before{content:'\2039'}.carousel-control .icon-next:before{content:'\203a'}.carousel-indicators{position:absolute;bottom:10px;left:50%;z-index:15;width:60%;margin-left:-30%;padding-left:0;list-style:none;text-align:center}.carousel-indicators li{display:inline-block;width:10px;height:10px;margin:1px;text-indent:-999px;border:1px solid #fff;border-radius:10px;cursor:pointer;background-color:transparent}.carousel-indicators .active{margin:0;width:12px;height:12px;background-color:#fff}.carousel-caption{position:absolute;left:15%;right:15%;bottom:20px;z-index:10;padding-top:20px;padding-bottom:20px;color:#fff;text-align:center;text-shadow:0 1px 2px rgba(0,0,0,.6)}.carousel-caption .btn{text-shadow:none}@media screen and (min-width:768px){.carousel-control .glyphicon-chevron-left,.carousel-control .glyphicon-chevron-right,.carousel-control .icon-next,.carousel-control .icon-prev{width:30px;height:30px;margin-top:-15px;font-size:30px}.carousel-control .glyphicon-chevron-left,.carousel-control .icon-prev{margin-left:-15px}.carousel-control .glyphicon-chevron-right,.carousel-control .icon-next{margin-right:-15px}.carousel-caption{left:20%;right:20%;padding-bottom:30px}.carousel-indicators{bottom:20px}}.btn-group-vertical>.btn-group:after,.btn-group-vertical>.btn-group:before,.btn-toolbar:after,.btn-toolbar:before,.clearfix:after,.clearfix:before,.container-fluid:after,.container-fluid:before,.container:after,.container:before,.dl-horizontal dd:after,.dl-horizontal dd:before,.form-horizontal .form-group:after,.form-horizontal .form-group:before,.item_buttons:after,.item_buttons:before,.modal-footer:after,.modal-footer:before,.nav:after,.nav:before,.navbar-collapse:after,.navbar-collapse:before,.navbar-header:after,.navbar-header:before,.navbar:after,.navbar:before,.pager:after,.pager:before,.panel-body:after,.panel-body:before,.row:after,.row:before{content:" ";display:table}.btn-group-vertical>.btn-group:after,.btn-toolbar:after,.clearfix:after,.container-fluid:after,.container:after,.dl-horizontal dd:after,.form-horizontal .form-group:after,.item_buttons:after,.modal-footer:after,.nav:after,.navbar-collapse:after,.navbar-header:after,.navbar:after,.pager:after,.panel-body:after,.row:after{clear:both}.center-block{display:block;margin-left:auto;margin-right:auto}.pull-right{float:right!important}.pull-left{float:left!important}.hide{display:none!important}.show{display:block!important}.invisible{visibility:hidden}.text-hide{font:0/0 a;color:transparent;text-shadow:none;background-color:transparent;border:0}.hidden{display:none!important}.affix{position:fixed}@-ms-viewport{width:device-width}.visible-lg,.visible-lg-block,.visible-lg-inline,.visible-lg-inline-block,.visible-md,.visible-md-block,.visible-md-inline,.visible-md-inline-block,.visible-sm,.visible-sm-block,.visible-sm-inline,.visible-sm-inline-block,.visible-xs,.visible-xs-block,.visible-xs-inline,.visible-xs-inline-block{display:none!important}@media (max-width:767px){.visible-xs{display:block!important}table.visible-xs{display:table}tr.visible-xs{display:table-row!important}td.visible-xs,th.visible-xs{display:table-cell!important}.visible-xs-block{display:block!important}.visible-xs-inline{display:inline!important}.visible-xs-inline-block{display:inline-block!important}}@media (min-width:768px)and (max-width:991px){.visible-sm{display:block!important}table.visible-sm{display:table}tr.visible-sm{display:table-row!important}td.visible-sm,th.visible-sm{display:table-cell!important}.visible-sm-block{display:block!important}.visible-sm-inline{display:inline!important}.visible-sm-inline-block{display:inline-block!important}}@media (min-width:992px)and (max-width:1199px){.visible-md{display:block!important}table.visible-md{display:table}tr.visible-md{display:table-row!important}td.visible-md,th.visible-md{display:table-cell!important}.visible-md-block{display:block!important}.visible-md-inline{display:inline!important}.visible-md-inline-block{display:inline-block!important}}@media (min-width:1200px){.visible-lg{display:block!important}table.visible-lg{display:table}tr.visible-lg{display:table-row!important}td.visible-lg,th.visible-lg{display:table-cell!important}.visible-lg-block{display:block!important}.visible-lg-inline{display:inline!important}.visible-lg-inline-block{display:inline-block!important}}@media (max-width:767px){.hidden-xs{display:none!important}}@media (min-width:768px)and (max-width:991px){.hidden-sm{display:none!important}}@media (min-width:992px)and (max-width:1199px){.hidden-md{display:none!important}}@media (min-width:1200px){.hidden-lg{display:none!important}}.visible-print{display:none!important}@media print{.visible-print{display:block!important}table.visible-print{display:table}tr.visible-print{display:table-row!important}td.visible-print,th.visible-print{display:table-cell!important}}.visible-print-block{display:none!important}@media print{.visible-print-block{display:block!important}}.visible-print-inline{display:none!important}@media print{.visible-print-inline{display:inline!important}}.visible-print-inline-block{display:none!important}@media print{.visible-print-inline-block{display:inline-block!important}.hidden-print{display:none!important}}/*!
*
* Font Awesome
*
*//*!
 *  Font Awesome 4.2.0 by @davegandy - http://fontawesome.io - @fontawesome
 *  License - http://fontawesome.io/license (Font: SIL OFL 1.1, CSS: MIT License)
 */@font-face{font-family:'FontAwesome';src:url(../components/font-awesome/fonts/fontawesome-webfont.eot?v=4.2.0);src:url(../components/font-awesome/fonts/fontawesome-webfont.eot?#iefix&v=4.2.0)format('embedded-opentype'),url(../components/font-awesome/fonts/fontawesome-webfont.woff?v=4.2.0)format('woff'),url(../components/font-awesome/fonts/fontawesome-webfont.ttf?v=4.2.0)format('truetype'),url(../components/font-awesome/fonts/fontawesome-webfont.svg?v=4.2.0#fontawesomeregular)format('svg');font-weight:400;font-style:normal}.fa{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale}.fa-lg{font-size:1.33333333em;line-height:.75em;vertical-align:-15%}.fa-2x{font-size:2em}.fa-3x{font-size:3em}.fa-4x{font-size:4em}.fa-5x{font-size:5em}.fa-fw{width:1.28571429em;text-align:center}.fa-ul{padding-left:0;margin-left:2.14285714em;list-style-type:none}.fa-ul>li{position:relative}.fa-li{position:absolute;left:-2.14285714em;width:2.14285714em;top:.14285714em;text-align:center}.fa-li.fa-lg{left:-1.85714286em}.fa-border{padding:.2em .25em .15em;border:.08em solid #eee;border-radius:.1em}.fa.pull-left{margin-right:.3em}.fa.pull-right{margin-left:.3em}.fa-spin{-webkit-animation:fa-spin 2s infinite linear;animation:fa-spin 2s infinite linear}@-webkit-keyframes fa-spin{0%{-webkit-transform:rotate(0);transform:rotate(0)}100%{-webkit-transform:rotate(359deg);transform:rotate(359deg)}}@keyframes fa-spin{0%{-webkit-transform:rotate(0);transform:rotate(0)}100%{-webkit-transform:rotate(359deg);transform:rotate(359deg)}}.fa-rotate-90{filter:progid:DXImageTransform.Microsoft.BasicImage(rotation=1);-webkit-transform:rotate(90deg);-ms-transform:rotate(90deg);transform:rotate(90deg)}.fa-rotate-180{filter:progid:DXImageTransform.Microsoft.BasicImage(rotation=2);-webkit-transform:rotate(180deg);-ms-transform:rotate(180deg);transform:rotate(180deg)}.fa-rotate-270{filter:progid:DXImageTransform.Microsoft.BasicImage(rotation=3);-webkit-transform:rotate(270deg);-ms-transform:rotate(270deg);transform:rotate(270deg)}.fa-flip-horizontal{filter:progid:DXImageTransform.Microsoft.BasicImage(rotation=0, mirror=1);-webkit-transform:scale(-1,1);-ms-transform:scale(-1,1);transform:scale(-1,1)}.fa-flip-vertical{filter:progid:DXImageTransform.Microsoft.BasicImage(rotation=2, mirror=1);-webkit-transform:scale(1,-1);-ms-transform:scale(1,-1);transform:scale(1,-1)}:root .fa-flip-horizontal,:root .fa-flip-vertical,:root .fa-rotate-180,:root .fa-rotate-270,:root .fa-rotate-90{filter:none}.fa-stack{position:relative;display:inline-block;width:2em;height:2em;line-height:2em;vertical-align:middle}.fa-stack-1x,.fa-stack-2x{position:absolute;left:0;width:100%;text-align:center}.fa-stack-1x{line-height:inherit}.fa-stack-2x{font-size:2em}.fa-inverse{color:#fff}.fa-glass:before{content:"\f000"}.fa-music:before{content:"\f001"}.fa-search:before{content:"\f002"}.fa-envelope-o:before{content:"\f003"}.fa-heart:before{content:"\f004"}.fa-star:before{content:"\f005"}.fa-star-o:before{content:"\f006"}.fa-user:before{content:"\f007"}.fa-film:before{content:"\f008"}.fa-th-large:before{content:"\f009"}.fa-th:before{content:"\f00a"}.fa-th-list:before{content:"\f00b"}.fa-check:before{content:"\f00c"}.fa-close:before,.fa-remove:before,.fa-times:before{content:"\f00d"}.fa-search-plus:before{content:"\f00e"}.fa-search-minus:before{content:"\f010"}.fa-power-off:before{content:"\f011"}.fa-signal:before{content:"\f012"}.fa-cog:before,.fa-gear:before{content:"\f013"}.fa-trash-o:before{content:"\f014"}.fa-home:before{content:"\f015"}.fa-file-o:before{content:"\f016"}.fa-clock-o:before{content:"\f017"}.fa-road:before{content:"\f018"}.fa-download:before{content:"\f019"}.fa-arrow-circle-o-down:before{content:"\f01a"}.fa-arrow-circle-o-up:before{content:"\f01b"}.fa-inbox:before{content:"\f01c"}.fa-play-circle-o:before{content:"\f01d"}.fa-repeat:before,.fa-rotate-right:before{content:"\f01e"}.fa-refresh:before{content:"\f021"}.fa-list-alt:before{content:"\f022"}.fa-lock:before{content:"\f023"}.fa-flag:before{content:"\f024"}.fa-headphones:before{content:"\f025"}.fa-volume-off:before{content:"\f026"}.fa-volume-down:before{content:"\f027"}.fa-volume-up:before{content:"\f028"}.fa-qrcode:before{content:"\f029"}.fa-barcode:before{content:"\f02a"}.fa-tag:before{content:"\f02b"}.fa-tags:before{content:"\f02c"}.fa-book:before{content:"\f02d"}.fa-bookmark:before{content:"\f02e"}.fa-print:before{content:"\f02f"}.fa-camera:before{content:"\f030"}.fa-font:before{content:"\f031"}.fa-bold:before{content:"\f032"}.fa-italic:before{content:"\f033"}.fa-text-height:before{content:"\f034"}.fa-text-width:before{content:"\f035"}.fa-align-left:before{content:"\f036"}.fa-align-center:before{content:"\f037"}.fa-align-right:before{content:"\f038"}.fa-align-justify:before{content:"\f039"}.fa-list:before{content:"\f03a"}.fa-dedent:before,.fa-outdent:before{content:"\f03b"}.fa-indent:before{content:"\f03c"}.fa-video-camera:before{content:"\f03d"}.fa-image:before,.fa-photo:before,.fa-picture-o:before{content:"\f03e"}.fa-pencil:before{content:"\f040"}.fa-map-marker:before{content:"\f041"}.fa-adjust:before{content:"\f042"}.fa-tint:before{content:"\f043"}.fa-edit:before,.fa-pencil-square-o:before{content:"\f044"}.fa-share-square-o:before{content:"\f045"}.fa-check-square-o:before{content:"\f046"}.fa-arrows:before{content:"\f047"}.fa-step-backward:before{content:"\f048"}.fa-fast-backward:before{content:"\f049"}.fa-backward:before{content:"\f04a"}.fa-play:before{content:"\f04b"}.fa-pause:before{content:"\f04c"}.fa-stop:before{content:"\f04d"}.fa-forward:before{content:"\f04e"}.fa-fast-forward:before{content:"\f050"}.fa-step-forward:before{content:"\f051"}.fa-eject:before{content:"\f052"}.fa-chevron-left:before{content:"\f053"}.fa-chevron-right:before{content:"\f054"}.fa-plus-circle:before{content:"\f055"}.fa-minus-circle:before{content:"\f056"}.fa-times-circle:before{content:"\f057"}.fa-check-circle:before{content:"\f058"}.fa-question-circle:before{content:"\f059"}.fa-info-circle:before{content:"\f05a"}.fa-crosshairs:before{content:"\f05b"}.fa-times-circle-o:before{content:"\f05c"}.fa-check-circle-o:before{content:"\f05d"}.fa-ban:before{content:"\f05e"}.fa-arrow-left:before{content:"\f060"}.fa-arrow-right:before{content:"\f061"}.fa-arrow-up:before{content:"\f062"}.fa-arrow-down:before{content:"\f063"}.fa-mail-forward:before,.fa-share:before{content:"\f064"}.fa-expand:before{content:"\f065"}.fa-compress:before{content:"\f066"}.fa-plus:before{content:"\f067"}.fa-minus:before{content:"\f068"}.fa-asterisk:before{content:"\f069"}.fa-exclamation-circle:before{content:"\f06a"}.fa-gift:before{content:"\f06b"}.fa-leaf:before{content:"\f06c"}.fa-fire:before{content:"\f06d"}.fa-eye:before{content:"\f06e"}.fa-eye-slash:before{content:"\f070"}.fa-exclamation-triangle:before,.fa-warning:before{content:"\f071"}.fa-plane:before{content:"\f072"}.fa-calendar:before{content:"\f073"}.fa-random:before{content:"\f074"}.fa-comment:before{content:"\f075"}.fa-magnet:before{content:"\f076"}.fa-chevron-up:before{content:"\f077"}.fa-chevron-down:before{content:"\f078"}.fa-retweet:before{content:"\f079"}.fa-shopping-cart:before{content:"\f07a"}.fa-folder:before{content:"\f07b"}.fa-folder-open:before{content:"\f07c"}.fa-arrows-v:before{content:"\f07d"}.fa-arrows-h:before{content:"\f07e"}.fa-bar-chart-o:before,.fa-bar-chart:before{content:"\f080"}.fa-twitter-square:before{content:"\f081"}.fa-facebook-square:before{content:"\f082"}.fa-camera-retro:before{content:"\f083"}.fa-key:before{content:"\f084"}.fa-cogs:before,.fa-gears:before{content:"\f085"}.fa-comments:before{content:"\f086"}.fa-thumbs-o-up:before{content:"\f087"}.fa-thumbs-o-down:before{content:"\f088"}.fa-star-half:before{content:"\f089"}.fa-heart-o:before{content:"\f08a"}.fa-sign-out:before{content:"\f08b"}.fa-linkedin-square:before{content:"\f08c"}.fa-thumb-tack:before{content:"\f08d"}.fa-external-link:before{content:"\f08e"}.fa-sign-in:before{content:"\f090"}.fa-trophy:before{content:"\f091"}.fa-github-square:before{content:"\f092"}.fa-upload:before{content:"\f093"}.fa-lemon-o:before{content:"\f094"}.fa-phone:before{content:"\f095"}.fa-square-o:before{content:"\f096"}.fa-bookmark-o:before{content:"\f097"}.fa-phone-square:before{content:"\f098"}.fa-twitter:before{content:"\f099"}.fa-facebook:before{content:"\f09a"}.fa-github:before{content:"\f09b"}.fa-unlock:before{content:"\f09c"}.fa-credit-card:before{content:"\f09d"}.fa-rss:before{content:"\f09e"}.fa-hdd-o:before{content:"\f0a0"}.fa-bullhorn:before{content:"\f0a1"}.fa-bell:before{content:"\f0f3"}.fa-certificate:before{content:"\f0a3"}.fa-hand-o-right:before{content:"\f0a4"}.fa-hand-o-left:before{content:"\f0a5"}.fa-hand-o-up:before{content:"\f0a6"}.fa-hand-o-down:before{content:"\f0a7"}.fa-arrow-circle-left:before{content:"\f0a8"}.fa-arrow-circle-right:before{content:"\f0a9"}.fa-arrow-circle-up:before{content:"\f0aa"}.fa-arrow-circle-down:before{content:"\f0ab"}.fa-globe:before{content:"\f0ac"}.fa-wrench:before{content:"\f0ad"}.fa-tasks:before{content:"\f0ae"}.fa-filter:before{content:"\f0b0"}.fa-briefcase:before{content:"\f0b1"}.fa-arrows-alt:before{content:"\f0b2"}.fa-group:before,.fa-users:before{content:"\f0c0"}.fa-chain:before,.fa-link:before{content:"\f0c1"}.fa-cloud:before{content:"\f0c2"}.fa-flask:before{content:"\f0c3"}.fa-cut:before,.fa-scissors:before{content:"\f0c4"}.fa-copy:before,.fa-files-o:before{content:"\f0c5"}.fa-paperclip:before{content:"\f0c6"}.fa-floppy-o:before,.fa-save:before{content:"\f0c7"}.fa-square:before{content:"\f0c8"}.fa-bars:before,.fa-navicon:before,.fa-reorder:before{content:"\f0c9"}.fa-list-ul:before{content:"\f0ca"}.fa-list-ol:before{content:"\f0cb"}.fa-strikethrough:before{content:"\f0cc"}.fa-underline:before{content:"\f0cd"}.fa-table:before{content:"\f0ce"}.fa-magic:before{content:"\f0d0"}.fa-truck:before{content:"\f0d1"}.fa-pinterest:before{content:"\f0d2"}.fa-pinterest-square:before{content:"\f0d3"}.fa-google-plus-square:before{content:"\f0d4"}.fa-google-plus:before{content:"\f0d5"}.fa-money:before{content:"\f0d6"}.fa-caret-down:before{content:"\f0d7"}.fa-caret-up:before{content:"\f0d8"}.fa-caret-left:before{content:"\f0d9"}.fa-caret-right:before{content:"\f0da"}.fa-columns:before{content:"\f0db"}.fa-sort:before,.fa-unsorted:before{content:"\f0dc"}.fa-sort-desc:before,.fa-sort-down:before{content:"\f0dd"}.fa-sort-asc:before,.fa-sort-up:before{content:"\f0de"}.fa-envelope:before{content:"\f0e0"}.fa-linkedin:before{content:"\f0e1"}.fa-rotate-left:before,.fa-undo:before{content:"\f0e2"}.fa-gavel:before,.fa-legal:before{content:"\f0e3"}.fa-dashboard:before,.fa-tachometer:before{content:"\f0e4"}.fa-comment-o:before{content:"\f0e5"}.fa-comments-o:before{content:"\f0e6"}.fa-bolt:before,.fa-flash:before{content:"\f0e7"}.fa-sitemap:before{content:"\f0e8"}.fa-umbrella:before{content:"\f0e9"}.fa-clipboard:before,.fa-paste:before{content:"\f0ea"}.fa-lightbulb-o:before{content:"\f0eb"}.fa-exchange:before{content:"\f0ec"}.fa-cloud-download:before{content:"\f0ed"}.fa-cloud-upload:before{content:"\f0ee"}.fa-user-md:before{content:"\f0f0"}.fa-stethoscope:before{content:"\f0f1"}.fa-suitcase:before{content:"\f0f2"}.fa-bell-o:before{content:"\f0a2"}.fa-coffee:before{content:"\f0f4"}.fa-cutlery:before{content:"\f0f5"}.fa-file-text-o:before{content:"\f0f6"}.fa-building-o:before{content:"\f0f7"}.fa-hospital-o:before{content:"\f0f8"}.fa-ambulance:before{content:"\f0f9"}.fa-medkit:before{content:"\f0fa"}.fa-fighter-jet:before{content:"\f0fb"}.fa-beer:before{content:"\f0fc"}.fa-h-square:before{content:"\f0fd"}.fa-plus-square:before{content:"\f0fe"}.fa-angle-double-left:before{content:"\f100"}.fa-angle-double-right:before{content:"\f101"}.fa-angle-double-up:before{content:"\f102"}.fa-angle-double-down:before{content:"\f103"}.fa-angle-left:before{content:"\f104"}.fa-angle-right:before{content:"\f105"}.fa-angle-up:before{content:"\f106"}.fa-angle-down:before{content:"\f107"}.fa-desktop:before{content:"\f108"}.fa-laptop:before{content:"\f109"}.fa-tablet:before{content:"\f10a"}.fa-mobile-phone:before,.fa-mobile:before{content:"\f10b"}.fa-circle-o:before{content:"\f10c"}.fa-quote-left:before{content:"\f10d"}.fa-quote-right:before{content:"\f10e"}.fa-spinner:before{content:"\f110"}.fa-circle:before{content:"\f111"}.fa-mail-reply:before,.fa-reply:before{content:"\f112"}.fa-github-alt:before{content:"\f113"}.fa-folder-o:before{content:"\f114"}.fa-folder-open-o:before{content:"\f115"}.fa-smile-o:before{content:"\f118"}.fa-frown-o:before{content:"\f119"}.fa-meh-o:before{content:"\f11a"}.fa-gamepad:before{content:"\f11b"}.fa-keyboard-o:before{content:"\f11c"}.fa-flag-o:before{content:"\f11d"}.fa-flag-checkered:before{content:"\f11e"}.fa-terminal:before{content:"\f120"}.fa-code:before{content:"\f121"}.fa-mail-reply-all:before,.fa-reply-all:before{content:"\f122"}.fa-star-half-empty:before,.fa-star-half-full:before,.fa-star-half-o:before{content:"\f123"}.fa-location-arrow:before{content:"\f124"}.fa-crop:before{content:"\f125"}.fa-code-fork:before{content:"\f126"}.fa-chain-broken:before,.fa-unlink:before{content:"\f127"}.fa-question:before{content:"\f128"}.fa-info:before{content:"\f129"}.fa-exclamation:before{content:"\f12a"}.fa-superscript:before{content:"\f12b"}.fa-subscript:before{content:"\f12c"}.fa-eraser:before{content:"\f12d"}.fa-puzzle-piece:before{content:"\f12e"}.fa-microphone:before{content:"\f130"}.fa-microphone-slash:before{content:"\f131"}.fa-shield:before{content:"\f132"}.fa-calendar-o:before{content:"\f133"}.fa-fire-extinguisher:before{content:"\f134"}.fa-rocket:before{content:"\f135"}.fa-maxcdn:before{content:"\f136"}.fa-chevron-circle-left:before{content:"\f137"}.fa-chevron-circle-right:before{content:"\f138"}.fa-chevron-circle-up:before{content:"\f139"}.fa-chevron-circle-down:before{content:"\f13a"}.fa-html5:before{content:"\f13b"}.fa-css3:before{content:"\f13c"}.fa-anchor:before{content:"\f13d"}.fa-unlock-alt:before{content:"\f13e"}.fa-bullseye:before{content:"\f140"}.fa-ellipsis-h:before{content:"\f141"}.fa-ellipsis-v:before{content:"\f142"}.fa-rss-square:before{content:"\f143"}.fa-play-circle:before{content:"\f144"}.fa-ticket:before{content:"\f145"}.fa-minus-square:before{content:"\f146"}.fa-minus-square-o:before{content:"\f147"}.fa-level-up:before{content:"\f148"}.fa-level-down:before{content:"\f149"}.fa-check-square:before{content:"\f14a"}.fa-pencil-square:before{content:"\f14b"}.fa-external-link-square:before{content:"\f14c"}.fa-share-square:before{content:"\f14d"}.fa-compass:before{content:"\f14e"}.fa-caret-square-o-down:before,.fa-toggle-down:before{content:"\f150"}.fa-caret-square-o-up:before,.fa-toggle-up:before{content:"\f151"}.fa-caret-square-o-right:before,.fa-toggle-right:before{content:"\f152"}.fa-eur:before,.fa-euro:before{content:"\f153"}.fa-gbp:before{content:"\f154"}.fa-dollar:before,.fa-usd:before{content:"\f155"}.fa-inr:before,.fa-rupee:before{content:"\f156"}.fa-cny:before,.fa-jpy:before,.fa-rmb:before,.fa-yen:before{content:"\f157"}.fa-rouble:before,.fa-rub:before,.fa-ruble:before{content:"\f158"}.fa-krw:before,.fa-won:before{content:"\f159"}.fa-bitcoin:before,.fa-btc:before{content:"\f15a"}.fa-file:before{content:"\f15b"}.fa-file-text:before{content:"\f15c"}.fa-sort-alpha-asc:before{content:"\f15d"}.fa-sort-alpha-desc:before{content:"\f15e"}.fa-sort-amount-asc:before{content:"\f160"}.fa-sort-amount-desc:before{content:"\f161"}.fa-sort-numeric-asc:before{content:"\f162"}.fa-sort-numeric-desc:before{content:"\f163"}.fa-thumbs-up:before{content:"\f164"}.fa-thumbs-down:before{content:"\f165"}.fa-youtube-square:before{content:"\f166"}.fa-youtube:before{content:"\f167"}.fa-xing:before{content:"\f168"}.fa-xing-square:before{content:"\f169"}.fa-youtube-play:before{content:"\f16a"}.fa-dropbox:before{content:"\f16b"}.fa-stack-overflow:before{content:"\f16c"}.fa-instagram:before{content:"\f16d"}.fa-flickr:before{content:"\f16e"}.fa-adn:before{content:"\f170"}.fa-bitbucket:before{content:"\f171"}.fa-bitbucket-square:before{content:"\f172"}.fa-tumblr:before{content:"\f173"}.fa-tumblr-square:before{content:"\f174"}.fa-long-arrow-down:before{content:"\f175"}.fa-long-arrow-up:before{content:"\f176"}.fa-long-arrow-left:before{content:"\f177"}.fa-long-arrow-right:before{content:"\f178"}.fa-apple:before{content:"\f179"}.fa-windows:before{content:"\f17a"}.fa-android:before{content:"\f17b"}.fa-linux:before{content:"\f17c"}.fa-dribbble:before{content:"\f17d"}.fa-skype:before{content:"\f17e"}.fa-foursquare:before{content:"\f180"}.fa-trello:before{content:"\f181"}.fa-female:before{content:"\f182"}.fa-male:before{content:"\f183"}.fa-gittip:before{content:"\f184"}.fa-sun-o:before{content:"\f185"}.fa-moon-o:before{content:"\f186"}.fa-archive:before{content:"\f187"}.fa-bug:before{content:"\f188"}.fa-vk:before{content:"\f189"}.fa-weibo:before{content:"\f18a"}.fa-renren:before{content:"\f18b"}.fa-pagelines:before{content:"\f18c"}.fa-stack-exchange:before{content:"\f18d"}.fa-arrow-circle-o-right:before{content:"\f18e"}.fa-arrow-circle-o-left:before{content:"\f190"}.fa-caret-square-o-left:before,.fa-toggle-left:before{content:"\f191"}.fa-dot-circle-o:before{content:"\f192"}.fa-wheelchair:before{content:"\f193"}.fa-vimeo-square:before{content:"\f194"}.fa-try:before,.fa-turkish-lira:before{content:"\f195"}.fa-plus-square-o:before{content:"\f196"}.fa-space-shuttle:before{content:"\f197"}.fa-slack:before{content:"\f198"}.fa-envelope-square:before{content:"\f199"}.fa-wordpress:before{content:"\f19a"}.fa-openid:before{content:"\f19b"}.fa-bank:before,.fa-institution:before,.fa-university:before{content:"\f19c"}.fa-graduation-cap:before,.fa-mortar-board:before{content:"\f19d"}.fa-yahoo:before{content:"\f19e"}.fa-google:before{content:"\f1a0"}.fa-reddit:before{content:"\f1a1"}.fa-reddit-square:before{content:"\f1a2"}.fa-stumbleupon-circle:before{content:"\f1a3"}.fa-stumbleupon:before{content:"\f1a4"}.fa-delicious:before{content:"\f1a5"}.fa-digg:before{content:"\f1a6"}.fa-pied-piper:before{content:"\f1a7"}.fa-pied-piper-alt:before{content:"\f1a8"}.fa-drupal:before{content:"\f1a9"}.fa-joomla:before{content:"\f1aa"}.fa-language:before{content:"\f1ab"}.fa-fax:before{content:"\f1ac"}.fa-building:before{content:"\f1ad"}.fa-child:before{content:"\f1ae"}.fa-paw:before{content:"\f1b0"}.fa-spoon:before{content:"\f1b1"}.fa-cube:before{content:"\f1b2"}.fa-cubes:before{content:"\f1b3"}.fa-behance:before{content:"\f1b4"}.fa-behance-square:before{content:"\f1b5"}.fa-steam:before{content:"\f1b6"}.fa-steam-square:before{content:"\f1b7"}.fa-recycle:before{content:"\f1b8"}.fa-automobile:before,.fa-car:before{content:"\f1b9"}.fa-cab:before,.fa-taxi:before{content:"\f1ba"}.fa-tree:before{content:"\f1bb"}.fa-spotify:before{content:"\f1bc"}.fa-deviantart:before{content:"\f1bd"}.fa-soundcloud:before{content:"\f1be"}.fa-database:before{content:"\f1c0"}.fa-file-pdf-o:before{content:"\f1c1"}.fa-file-word-o:before{content:"\f1c2"}.fa-file-excel-o:before{content:"\f1c3"}.fa-file-powerpoint-o:before{content:"\f1c4"}.fa-file-image-o:before,.fa-file-photo-o:before,.fa-file-picture-o:before{content:"\f1c5"}.fa-file-archive-o:before,.fa-file-zip-o:before{content:"\f1c6"}.fa-file-audio-o:before,.fa-file-sound-o:before{content:"\f1c7"}.fa-file-movie-o:before,.fa-file-video-o:before{content:"\f1c8"}.fa-file-code-o:before{content:"\f1c9"}.fa-vine:before{content:"\f1ca"}.fa-codepen:before{content:"\f1cb"}.fa-jsfiddle:before{content:"\f1cc"}.fa-life-bouy:before,.fa-life-buoy:before,.fa-life-ring:before,.fa-life-saver:before,.fa-support:before{content:"\f1cd"}.fa-circle-o-notch:before{content:"\f1ce"}.fa-ra:before,.fa-rebel:before{content:"\f1d0"}.fa-empire:before,.fa-ge:before{content:"\f1d1"}.fa-git-square:before{content:"\f1d2"}.fa-git:before{content:"\f1d3"}.fa-hacker-news:before{content:"\f1d4"}.fa-tencent-weibo:before{content:"\f1d5"}.fa-qq:before{content:"\f1d6"}.fa-wechat:before,.fa-weixin:before{content:"\f1d7"}.fa-paper-plane:before,.fa-send:before{content:"\f1d8"}.fa-paper-plane-o:before,.fa-send-o:before{content:"\f1d9"}.fa-history:before{content:"\f1da"}.fa-circle-thin:before{content:"\f1db"}.fa-header:before{content:"\f1dc"}.fa-paragraph:before{content:"\f1dd"}.fa-sliders:before{content:"\f1de"}.fa-share-alt:before{content:"\f1e0"}.fa-share-alt-square:before{content:"\f1e1"}.fa-bomb:before{content:"\f1e2"}.fa-futbol-o:before,.fa-soccer-ball-o:before{content:"\f1e3"}.fa-tty:before{content:"\f1e4"}.fa-binoculars:before{content:"\f1e5"}.fa-plug:before{content:"\f1e6"}.fa-slideshare:before{content:"\f1e7"}.fa-twitch:before{content:"\f1e8"}.fa-yelp:before{content:"\f1e9"}.fa-newspaper-o:before{content:"\f1ea"}.fa-wifi:before{content:"\f1eb"}.fa-calculator:before{content:"\f1ec"}.fa-paypal:before{content:"\f1ed"}.fa-google-wallet:before{content:"\f1ee"}.fa-cc-visa:before{content:"\f1f0"}.fa-cc-mastercard:before{content:"\f1f1"}.fa-cc-discover:before{content:"\f1f2"}.fa-cc-amex:before{content:"\f1f3"}.fa-cc-paypal:before{content:"\f1f4"}.fa-cc-stripe:before{content:"\f1f5"}.fa-bell-slash:before{content:"\f1f6"}.fa-bell-slash-o:before{content:"\f1f7"}.fa-trash:before{content:"\f1f8"}.fa-copyright:before{content:"\f1f9"}.fa-at:before{content:"\f1fa"}.fa-eyedropper:before{content:"\f1fb"}.fa-paint-brush:before{content:"\f1fc"}.fa-birthday-cake:before{content:"\f1fd"}.fa-area-chart:before{content:"\f1fe"}.fa-pie-chart:before{content:"\f200"}.fa-line-chart:before{content:"\f201"}.fa-lastfm:before{content:"\f202"}.fa-lastfm-square:before{content:"\f203"}.fa-toggle-off:before{content:"\f204"}.fa-toggle-on:before{content:"\f205"}.fa-bicycle:before{content:"\f206"}.fa-bus:before{content:"\f207"}.fa-ioxhost:before{content:"\f208"}.fa-angellist:before{content:"\f209"}.fa-cc:before{content:"\f20a"}.fa-ils:before,.fa-shekel:before,.fa-sheqel:before{content:"\f20b"}.fa-meanpath:before{content:"\f20c"}/*!
*
* IPython base
*
*/.modal.fade .modal-dialog{-webkit-transform:translate(0,0);-ms-transform:translate(0,0);-o-transform:translate(0,0);transform:translate(0,0)}code{color:#000}pre{font-size:inherit;line-height:inherit}label{font-weight:400}.border-box-sizing{box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box}.corner-all{border-radius:2px}.no-padding{padding:0}.hbox{display:-webkit-box;-webkit-box-orient:horizontal;display:-moz-box;-moz-box-orient:horizontal;display:box;box-orient:horizontal;box-align:stretch;display:flex;flex-direction:row;align-items:stretch}.hbox>*{-webkit-box-flex:0;-moz-box-flex:0;box-flex:0;flex:none}.vbox{display:-webkit-box;-webkit-box-orient:vertical;display:-moz-box;-moz-box-orient:vertical;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch}.vbox>*{-webkit-box-flex:0;-moz-box-flex:0;box-flex:0;flex:none}.hbox.reverse,.reverse,.vbox.reverse{-webkit-box-direction:reverse;-moz-box-direction:reverse;box-direction:reverse;flex-direction:row-reverse}.box-flex0,.hbox.box-flex0,.vbox.box-flex0{-webkit-box-flex:0;-moz-box-flex:0;box-flex:0;flex:none;width:auto}.box-flex1,.hbox.box-flex1,.vbox.box-flex1{-webkit-box-flex:1;-moz-box-flex:1;box-flex:1;flex:1}.box-flex,.hbox.box-flex,.vbox.box-flex{-webkit-box-flex:1;-moz-box-flex:1;box-flex:1;flex:1}.box-flex2,.hbox.box-flex2,.vbox.box-flex2{-webkit-box-flex:2;-moz-box-flex:2;box-flex:2;flex:2}.box-group1{-webkit-box-flex-group:1;-moz-box-flex-group:1;box-flex-group:1}.box-group2{-webkit-box-flex-group:2;-moz-box-flex-group:2;box-flex-group:2}.hbox.start,.start,.vbox.start{-webkit-box-pack:start;-moz-box-pack:start;box-pack:start;justify-content:flex-start}.end,.hbox.end,.vbox.end{-webkit-box-pack:end;-moz-box-pack:end;box-pack:end;justify-content:flex-end}.center,.hbox.center,.vbox.center{-webkit-box-pack:center;-moz-box-pack:center;box-pack:center;justify-content:center}.baseline,.hbox.baseline,.vbox.baseline{-webkit-box-pack:baseline;-moz-box-pack:baseline;box-pack:baseline;justify-content:baseline}.hbox.stretch,.stretch,.vbox.stretch{-webkit-box-pack:stretch;-moz-box-pack:stretch;box-pack:stretch;justify-content:stretch}.align-start,.hbox.align-start,.vbox.align-start{-webkit-box-align:start;-moz-box-align:start;box-align:start;align-items:flex-start}.align-end,.hbox.align-end,.vbox.align-end{-webkit-box-align:end;-moz-box-align:end;box-align:end;align-items:flex-end}.align-center,.hbox.align-center,.vbox.align-center{-webkit-box-align:center;-moz-box-align:center;box-align:center;align-items:center}.align-baseline,.hbox.align-baseline,.vbox.align-baseline{-webkit-box-align:baseline;-moz-box-align:baseline;box-align:baseline;align-items:baseline}.align-stretch,.hbox.align-stretch,.vbox.align-stretch{-webkit-box-align:stretch;-moz-box-align:stretch;box-align:stretch;align-items:stretch}div.error{margin:2em;text-align:center}div.error>h1{font-size:500%;line-height:normal}div.error>p{font-size:200%;line-height:normal}div.traceback-wrapper{text-align:left;max-width:800px;margin:auto}body{position:absolute;left:0;right:0;top:0;bottom:0;overflow:visible}#header{display:none;background-color:#fff;position:relative;z-index:100}#header #header-container{padding-bottom:5px;padding-top:5px;box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box}#header .header-bar{width:100%;height:1px;background:#e7e7e7;margin-bottom:-1px}#header-spacer{width:100%;visibility:hidden}@media print{#header{display:none!important}#header-spacer{display:none}}#ipython_notebook{padding-left:0;padding-top:1px;padding-bottom:1px}@media (max-width:991px){#ipython_notebook{margin-left:10px}}#noscript{width:auto;padding-top:16px;padding-bottom:16px;text-align:center;font-size:22px;color:red;font-weight:700}#ipython_notebook img{height:28px}#site{width:100%;display:none;box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box;overflow:auto}@media print{#site{height:auto!important}}.ui-button .ui-button-text{padding:.2em .8em;font-size:77%}input.ui-button{padding:.3em .9em}span#login_widget{float:right}#logout,span#login_widget>.button{color:#333;background-color:#fff;border-color:#ccc}#logout.active,#logout.focus,#logout:active,#logout:focus,#logout:hover,.open>.dropdown-toggle#logout,.open>.dropdown-togglespan#login_widget>.button,span#login_widget>.button.active,span#login_widget>.button.focus,span#login_widget>.button:active,span#login_widget>.button:focus,span#login_widget>.button:hover{color:#333;background-color:#e6e6e6;border-color:#adadad}#logout.active,#logout:active,.open>.dropdown-toggle#logout,.open>.dropdown-togglespan#login_widget>.button,span#login_widget>.button.active,span#login_widget>.button:active{background-image:none}#logout.disabled,#logout.disabled.active,#logout.disabled.focus,#logout.disabled:active,#logout.disabled:focus,#logout.disabled:hover,#logout[disabled],#logout[disabled].active,#logout[disabled].focus,#logout[disabled]:active,#logout[disabled]:focus,#logout[disabled]:hover,fieldset[disabled] #logout,fieldset[disabled] #logout.active,fieldset[disabled] #logout.focus,fieldset[disabled] #logout:active,fieldset[disabled] #logout:focus,fieldset[disabled] #logout:hover,fieldset[disabled] span#login_widget>.button,fieldset[disabled] span#login_widget>.button.active,fieldset[disabled] span#login_widget>.button.focus,fieldset[disabled] span#login_widget>.button:active,fieldset[disabled] span#login_widget>.button:focus,fieldset[disabled] span#login_widget>.button:hover,span#login_widget>.button.disabled,span#login_widget>.button.disabled.active,span#login_widget>.button.disabled.focus,span#login_widget>.button.disabled:active,span#login_widget>.button.disabled:focus,span#login_widget>.button.disabled:hover,span#login_widget>.button[disabled],span#login_widget>.button[disabled].active,span#login_widget>.button[disabled].focus,span#login_widget>.button[disabled]:active,span#login_widget>.button[disabled]:focus,span#login_widget>.button[disabled]:hover{background-color:#fff;border-color:#ccc}#logout .badge,span#login_widget>.button .badge{color:#fff;background-color:#333}.nav-header{text-transform:none}#header>span{margin-top:10px}.modal_stretch .modal-dialog{display:-webkit-box;-webkit-box-orient:vertical;display:-moz-box;-moz-box-orient:vertical;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch;min-height:80vh}.modal_stretch .modal-dialog .modal-body{max-height:calc(100vh - 200px);overflow:auto;flex:1}@media (min-width:768px){.modal .modal-dialog{width:700px}select.form-control{margin-left:12px;margin-right:12px}}/*!
*
* IPython auth
*
*/.center-nav{display:inline-block;margin-bottom:-4px}/*!
*
* IPython tree view
*
*/.alternate_upload{background-color:none;display:inline}.alternate_upload.form{padding:0;margin:0}.alternate_upload input.fileinput{text-align:center;vertical-align:middle;display:inline;opacity:0;z-index:2;width:12ex;margin-right:-12ex}.alternate_upload .btn-upload{height:22px}ul#tabs{margin-bottom:4px}ul#tabs a{padding-top:6px;padding-bottom:4px}ul.breadcrumb a:focus,ul.breadcrumb a:hover{text-decoration:none}ul.breadcrumb i.icon-home{font-size:16px;margin-right:4px}ul.breadcrumb span{color:#5e5e5e}.list_toolbar{padding:4px 0;vertical-align:middle}.list_toolbar .tree-buttons{padding-top:1px}.dynamic-buttons{padding-top:3px;display:inline-block}.list_toolbar [class*=span]{min-height:24px}.list_header{font-weight:700;background-color:#eee}.list_placeholder{font-weight:700;padding:4px 7px}.list_container{margin-top:4px;margin-bottom:20px;border:1px solid #ddd;border-radius:2px}.list_container>div{border-bottom:1px solid #ddd}.list_container>div:hover .list-item{background-color:red}.list_container>div:last-child{border:none}.list_item:hover .list_item{background-color:#ddd}.list_item a{text-decoration:none}.list_item:hover{background-color:#fafafa}.action_col{text-align:right}.list_header>div,.list_item>div{line-height:22px;padding:4px 7px}.list_header>div input,.list_item>div input{margin-right:7px;margin-left:14px;vertical-align:baseline;line-height:22px;position:relative;top:-1px}.list_header>div .item_link,.list_item>div .item_link{margin-left:-1px;vertical-align:baseline;line-height:22px}.new-file input[type=checkbox]{visibility:hidden}.item_name{line-height:22px;height:24px}.item_icon{font-size:14px;color:#5e5e5e;margin-right:7px;margin-left:7px;line-height:22px;vertical-align:baseline}.item_buttons{line-height:1em;margin-left:-5px}.item_buttons .btn-group,.item_buttons .input-group{float:left}.item_buttons>.btn,.item_buttons>.btn-group,.item_buttons>.input-group{margin-left:5px}.item_buttons .btn{min-width:13ex}.item_buttons .running-indicator{padding-top:4px;color:#5cb85c}.toolbar_info{height:24px;line-height:24px}input.engine_num_input,input.nbname_input{padding-top:3px;padding-bottom:3px;height:22px;line-height:14px;margin:0}input.engine_num_input{width:60px}.highlight_text{color:#00f}#project_name{display:inline-block;padding-left:7px;margin-left:-2px}#project_name>.breadcrumb{padding:0;margin-bottom:0;background-color:transparent;font-weight:700}#tree-selector{padding-right:0}#button-select-all{min-width:50px}#select-all{margin-left:7px;margin-right:2px}.menu_icon{margin-right:2px}.tab-content .row{margin-left:0;margin-right:0}.folder_icon:before{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;content:"\f114"}.folder_icon:before.pull-left{margin-right:.3em}.folder_icon:before.pull-right{margin-left:.3em}.notebook_icon:before{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;content:"\f02d";position:relative;top:-1px}.notebook_icon:before.pull-left{margin-right:.3em}.notebook_icon:before.pull-right{margin-left:.3em}.running_notebook_icon:before{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;content:"\f02d";position:relative;top:-1px;color:#5cb85c}.running_notebook_icon:before.pull-left{margin-right:.3em}.running_notebook_icon:before.pull-right{margin-left:.3em}.file_icon:before{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;content:"\f016";position:relative;top:-2px}.file_icon:before.pull-left{margin-right:.3em}.file_icon:before.pull-right{margin-left:.3em}#notebook_toolbar .pull-right{padding-top:0;margin-right:-1px}ul#new-menu{left:auto;right:0}.kernel-menu-icon{padding-right:12px;width:24px;content:"\f096"}.kernel-menu-icon:before{content:"\f096"}.kernel-menu-icon-current:before{content:"\f00c"}#tab_content{padding-top:20px}#running .panel-group .panel{margin-top:3px;margin-bottom:1em}#running .panel-group .panel .panel-heading{background-color:#eee;line-height:22px;padding:4px 7px}#running .panel-group .panel .panel-heading a:focus,#running .panel-group .panel .panel-heading a:hover{text-decoration:none}#running .panel-group .panel .panel-body{padding:0}#running .panel-group .panel .panel-body .list_container{margin-top:0;margin-bottom:0;border:0;border-radius:0}#running .panel-group .panel .panel-body .list_container .list_item{border-bottom:1px solid #ddd}#running .panel-group .panel .panel-body .list_container .list_item:last-child{border-bottom:0}.delete-button,.duplicate-button,.rename-button,.shutdown-button{display:none}.dynamic-instructions{display:inline-block;padding-top:4px}/*!
*
* IPython text editor webapp
*
*/.selected-keymap i.fa{padding:0 5px}.selected-keymap i.fa:before{content:"\f00c"}#mode-menu{overflow:auto;max-height:20em}.edit_app #header{-webkit-box-shadow:0 0 12px 1px rgba(87,87,87,.2);box-shadow:0 0 12px 1px rgba(87,87,87,.2)}.edit_app #menubar .navbar{margin-bottom:-1px}.dirty-indicator{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;width:20px}.dirty-indicator.pull-left{margin-right:.3em}.dirty-indicator.pull-right{margin-left:.3em}.dirty-indicator-dirty{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;width:20px}.dirty-indicator-dirty.pull-left{margin-right:.3em}.dirty-indicator-dirty.pull-right{margin-left:.3em}.dirty-indicator-clean{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;width:20px}.dirty-indicator-clean.pull-left{margin-right:.3em}.dirty-indicator-clean.pull-right{margin-left:.3em}.dirty-indicator-clean:before{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;content:"\f00c"}.dirty-indicator-clean:before.pull-left{margin-right:.3em}.dirty-indicator-clean:before.pull-right{margin-left:.3em}#filename{font-size:16pt;display:table;padding:0 5px}#current-mode{padding-left:5px;padding-right:5px}#texteditor-backdrop{padding-top:20px;padding-bottom:20px}@media not print{#texteditor-backdrop{background-color:#eee}}@media print{#texteditor-backdrop #texteditor-container .CodeMirror-gutter,#texteditor-backdrop #texteditor-container .CodeMirror-gutters{background-color:#fff}}@media not print{#texteditor-backdrop #texteditor-container .CodeMirror-gutter,#texteditor-backdrop #texteditor-container .CodeMirror-gutters{background-color:#fff}#texteditor-backdrop #texteditor-container{padding:0;background-color:#fff;-webkit-box-shadow:0 0 12px 1px rgba(87,87,87,.2);box-shadow:0 0 12px 1px rgba(87,87,87,.2)}}/*!
*
* IPython notebook
*
*/.ansibold{font-weight:700}.ansiblack{color:#000}.ansired{color:#8b0000}.ansigreen{color:#006400}.ansiyellow{color:#c4a000}.ansiblue{color:#00008b}.ansipurple{color:#9400d3}.ansicyan{color:#4682b4}.ansigray{color:gray}.ansibgblack{background-color:#000}.ansibgred{background-color:red}.ansibggreen{background-color:green}.ansibgyellow{background-color:#ff0}.ansibgblue{background-color:#00f}.ansibgpurple{background-color:#ff00ff}.ansibgcyan{background-color:#0ff}.ansibggray{background-color:gray}div.cell{border:1px solid transparent;display:-webkit-box;-webkit-box-orient:vertical;display:-moz-box;-moz-box-orient:vertical;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch;border-radius:2px;box-sizing:border-box;-moz-box-sizing:border-box;border-width:thin;border-style:solid;width:100%;padding:5px;margin:0;outline:0}div.cell.selected{border-color:#ababab}@media print{div.cell.selected{border-color:transparent}}.edit_mode div.cell.selected{border-color:green}.prompt{min-width:14ex;padding:.4em;margin:0;font-family:monospace;text-align:right;line-height:1.21429em}div.inner_cell{display:-webkit-box;-webkit-box-orient:vertical;display:-moz-box;-moz-box-orient:vertical;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch;-webkit-box-flex:1;-moz-box-flex:1;box-flex:1;flex:1}@-moz-document url-prefix(){div.inner_cell{overflow-x:hidden}}div.input_area{border:1px solid #cfcfcf;border-radius:2px;background:#f7f7f7;line-height:1.21429em}div.prompt:empty{padding-top:0;padding-bottom:0}div.unrecognized_cell{padding:5px 5px 5px 0;display:-webkit-box;-webkit-box-orient:horizontal;display:-moz-box;-moz-box-orient:horizontal;display:box;box-orient:horizontal;box-align:stretch;display:flex;flex-direction:row;align-items:stretch}div.unrecognized_cell .inner_cell{border-radius:2px;padding:5px;font-weight:700;color:red;border:1px solid #cfcfcf;background:#eaeaea}div.unrecognized_cell .inner_cell a,div.unrecognized_cell .inner_cell a:hover{color:inherit;text-decoration:none}@media (max-width:540px){.prompt{text-align:left}div.unrecognized_cell>div.prompt{display:none}}div.code_cell{}div.input{page-break-inside:avoid;display:-webkit-box;-webkit-box-orient:horizontal;display:-moz-box;-moz-box-orient:horizontal;display:box;box-orient:horizontal;box-align:stretch;display:flex;flex-direction:row;align-items:stretch}@media (max-width:540px){div.input{-webkit-box-orient:vertical;-moz-box-orient:vertical;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch}}div.input_prompt{color:navy;border-top:1px solid transparent}div.input_area>div.highlight{margin:.4em;border:none;padding:0;background-color:transparent}div.input_area>div.highlight>pre{margin:0;border:none;padding:0;background-color:transparent}.CodeMirror{line-height:1.21429em;font-size:14px;height:auto;background:0 0}.CodeMirror-scroll{overflow-y:hidden;overflow-x:auto}.CodeMirror-lines{padding:.4em}.CodeMirror-linenumber{padding:0 8px 0 4px}.CodeMirror-gutters{border-bottom-left-radius:2px;border-top-left-radius:2px}.CodeMirror pre{padding:0;border:0;border-radius:0}.highlight-base,.highlight-variable{color:#000}.highlight-variable-2{color:#1a1a1a}.highlight-variable-3{color:#333}.highlight-string{color:#BA2121}.highlight-comment{color:#408080;font-style:italic}.highlight-number{color:#080}.highlight-atom{color:#88F}.highlight-keyword{color:green;font-weight:700}.highlight-builtin{color:green}.highlight-error{color:red}.highlight-operator{color:#A2F;font-weight:700}.highlight-meta{color:#A2F}.highlight-def{color:#00f}.highlight-string-2{color:#f50}.highlight-qualifier{color:#555}.highlight-bracket{color:#997}.highlight-tag{color:#170}.highlight-attribute{color:#00c}.highlight-header{color:#00f}.highlight-quote{color:#090}.highlight-link{color:#00c}.cm-s-ipython span.cm-keyword{color:green;font-weight:700}.cm-s-ipython span.cm-atom{color:#88F}.cm-s-ipython span.cm-number{color:#080}.cm-s-ipython span.cm-def{color:#00f}.cm-s-ipython span.cm-variable{color:#000}.cm-s-ipython span.cm-operator{color:#A2F;font-weight:700}.cm-s-ipython span.cm-variable-2{color:#1a1a1a}.cm-s-ipython span.cm-variable-3{color:#333}.cm-s-ipython span.cm-comment{color:#408080;font-style:italic}.cm-s-ipython span.cm-string{color:#BA2121}.cm-s-ipython span.cm-string-2{color:#f50}.cm-s-ipython span.cm-meta{color:#A2F}.cm-s-ipython span.cm-qualifier{color:#555}.cm-s-ipython span.cm-builtin{color:green}.cm-s-ipython span.cm-bracket{color:#997}.cm-s-ipython span.cm-tag{color:#170}.cm-s-ipython span.cm-attribute{color:#00c}.cm-s-ipython span.cm-header{color:#00f}.cm-s-ipython span.cm-quote{color:#090}.cm-s-ipython span.cm-link{color:#00c}.cm-s-ipython span.cm-error{color:red}.cm-s-ipython span.cm-tab{background:url('data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADAAAAAMCAYAAAAkuj5RAAAAAXNSR0IArs4c6QAAAGFJREFUSMft1LsRQFAQheHPowAKoACx3IgEKtaEHujDjORSgWTH/ZOdnZOcM/sgk/kFFWY0qV8foQwS4MKBCS3qR6ixBJvElOobYAtivseIE120FaowJPN75GMu8j/LfMwNjh4HUpwg4LUAAAAASUVORK5CYII=')right no-repeat}div.output_wrapper{display:-webkit-box;-webkit-box-align:stretch;display:-moz-box;-moz-box-align:stretch;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch;z-index:1}div.output_scroll{height:24em;width:100%;overflow:auto;border-radius:2px;-webkit-box-shadow:inset 0 2px 8px rgba(0,0,0,.8);box-shadow:inset 0 2px 8px rgba(0,0,0,.8);display:block}div.output_collapsed{margin:0;padding:0;display:-webkit-box;-webkit-box-orient:vertical;display:-moz-box;-moz-box-orient:vertical;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch}div.out_prompt_overlay{height:100%;padding:0 .4em;position:absolute;border-radius:2px}div.out_prompt_overlay:hover{-webkit-box-shadow:inset 0 0 1px #000;box-shadow:inset 0 0 1px #000;background:rgba(240,240,240,.5)}div.output_prompt{color:#8b0000}div.output_area{padding:0;page-break-inside:avoid;display:-webkit-box;-webkit-box-orient:horizontal;display:-moz-box;-moz-box-orient:horizontal;display:box;box-orient:horizontal;box-align:stretch;display:flex;flex-direction:row;align-items:stretch}div.output_area .MathJax_Display{text-align:left!important}div.output_area .rendered_html img,div.output_area .rendered_html table{margin-left:0;margin-right:0}div.output_area img,div.output_area svg{max-width:100%;height:auto}div.output_area img.unconfined,div.output_area svg.unconfined{max-width:none}.output{display:-webkit-box;-webkit-box-orient:vertical;display:-moz-box;-moz-box-orient:vertical;display:box;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch}@media (max-width:540px){div.output_area{-webkit-box-orient:vertical;-moz-box-orient:vertical;box-orient:vertical;box-align:stretch;display:flex;flex-direction:column;align-items:stretch}}div.output_area pre{margin:0;padding:0;border:0;vertical-align:baseline;color:#000;background-color:transparent;border-radius:0}div.output_subarea{overflow-x:auto;padding:.4em;-webkit-box-flex:1;-moz-box-flex:1;box-flex:1;flex:1;max-width:calc(100% - 14ex)}div.output_text{text-align:left;color:#000;line-height:1.21429em}div.output_stderr{background:#fdd}div.output_latex{text-align:left}div.output_javascript:empty{padding:0}.js-error{color:#8b0000}div.raw_input_container{font-family:monospace;padding-top:5px}span.raw_input_prompt{}input.raw_input{font-family:inherit;font-size:inherit;color:inherit;width:auto;vertical-align:baseline;padding:0 .25em;margin:0 .25em}input.raw_input:focus{box-shadow:none}p.p-space{margin-bottom:10px}div.output_unrecognized{padding:5px;font-weight:700;color:red}div.output_unrecognized a,div.output_unrecognized a:hover{color:inherit;text-decoration:none}.rendered_html{color:#000}.rendered_html em{font-style:italic}.rendered_html strong{font-weight:700}.rendered_html :link,.rendered_html :visited,.rendered_html u{text-decoration:underline}.rendered_html h1{font-size:185.7%;margin:1.08em 0 0;font-weight:700;line-height:1}.rendered_html h2{font-size:157.1%;margin:1.27em 0 0;font-weight:700;line-height:1}.rendered_html h3{font-size:128.6%;margin:1.55em 0 0;font-weight:700;line-height:1}.rendered_html h4{font-size:100%;margin:2em 0 0;font-weight:700;line-height:1}.rendered_html h5,.rendered_html h6{font-size:100%;margin:2em 0 0;font-weight:700;line-height:1;font-style:italic}.rendered_html h1:first-child{margin-top:.538em}.rendered_html h2:first-child{margin-top:.636em}.rendered_html h3:first-child{margin-top:.777em}.rendered_html h4:first-child,.rendered_html h5:first-child,.rendered_html h6:first-child{margin-top:1em}.rendered_html ul{list-style:disc;margin:0 2em;padding-left:0}.rendered_html ul ul{list-style:square;margin:0 2em}.rendered_html ul ul ul{list-style:circle;margin:0 2em}.rendered_html ol{list-style:decimal;margin:0 2em;padding-left:0}.rendered_html ol ol{list-style:upper-alpha;margin:0 2em}.rendered_html ol ol ol{list-style:lower-alpha;margin:0 2em}.rendered_html ol ol ol ol{list-style:lower-roman;margin:0 2em}.rendered_html ol ol ol ol ol{list-style:decimal;margin:0 2em}.rendered_html *+ol,.rendered_html *+ul{margin-top:1em}.rendered_html hr{color:#000;background-color:#000}.rendered_html pre{margin:1em 2em}.rendered_html code,.rendered_html pre{border:0;background-color:#fff;color:#000;font-size:100%;padding:0}.rendered_html blockquote{margin:1em 2em}.rendered_html table{margin-left:auto;margin-right:auto;border:1px solid #000;border-collapse:collapse}.rendered_html td,.rendered_html th,.rendered_html tr{border:1px solid #000;border-collapse:collapse;margin:1em 2em}.rendered_html td,.rendered_html th{text-align:left;vertical-align:middle;padding:4px}.rendered_html th{font-weight:700}.rendered_html *+table{margin-top:1em}.rendered_html p{text-align:left}.rendered_html *+p{margin-top:1em}.rendered_html img{display:block;margin-left:auto;margin-right:auto}.rendered_html *+img{margin-top:1em}.rendered_html img,.rendered_html svg{max-width:100%;height:auto}.rendered_html img.unconfined,.rendered_html svg.unconfined{max-width:none}div.text_cell{display:-webkit-box;-webkit-box-orient:horizontal;display:-moz-box;-moz-box-orient:horizontal;display:box;box-orient:horizontal;box-align:stretch;display:flex;flex-direction:row;align-items:stretch}@media (max-width:540px){div.text_cell>div.prompt{display:none}}div.text_cell_render{outline:0;resize:none;width:inherit;border-style:none;padding:.5em .5em .5em .4em;color:#000;box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box}a.anchor-link:link{text-decoration:none;padding:0 20px;visibility:hidden}h1:hover .anchor-link,h2:hover .anchor-link,h3:hover .anchor-link,h4:hover .anchor-link,h5:hover .anchor-link,h6:hover .anchor-link{visibility:visible}.text_cell.rendered .input_area{display:none}.text_cell.rendered .rendered_html{overflow-x:auto}.text_cell.unrendered .text_cell_render{display:none}.cm-header-1,.cm-header-2,.cm-header-3,.cm-header-4,.cm-header-5,.cm-header-6{font-weight:700;font-family:"Helvetica Neue",Helvetica,Arial,sans-serif}.cm-header-1{font-size:185.7%}.cm-header-2{font-size:157.1%}.cm-header-3{font-size:128.6%}.cm-header-4{font-size:110%}.cm-header-5,.cm-header-6{font-size:100%;font-style:italic}/*!
*
* IPython notebook webapp
*
*/@media (max-width:767px){.notebook_app{padding-left:0;padding-right:0}}#ipython-main-app{box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box;height:100%}div#notebook_panel{margin:0;padding:0;box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box;height:100%}#notebook{font-size:14px;line-height:20px;overflow-y:hidden;overflow-x:auto;width:100%;padding-top:20px;margin:0;outline:0;box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box;min-height:100%}@media not print{#notebook-container{padding:15px;background-color:#fff;min-height:0;-webkit-box-shadow:0 0 12px 1px rgba(87,87,87,.2);box-shadow:0 0 12px 1px rgba(87,87,87,.2)}}div.ui-widget-content{border:1px solid #ababab;outline:0}pre.dialog{background-color:#f7f7f7;border:1px solid #ddd;border-radius:2px;padding:.4em .4em .4em 2em}p.dialog{padding:.2em}code,kbd,pre,samp{white-space:pre-wrap}#fonttest{font-family:monospace}p{margin-bottom:0}.end_space{min-height:100px;transition:height .2s ease}.notebook_app #header{-webkit-box-shadow:0 0 12px 1px rgba(87,87,87,.2);box-shadow:0 0 12px 1px rgba(87,87,87,.2)}@media not print{.notebook_app{background-color:#eee}}.celltoolbar{border:thin solid #CFCFCF;border-bottom:none;background:#EEE;border-radius:2px 2px 0 0;width:100%;height:29px;padding-right:4px;-webkit-box-orient:horizontal;-moz-box-orient:horizontal;box-orient:horizontal;box-align:stretch;display:flex;flex-direction:row;align-items:stretch;-webkit-box-pack:end;-moz-box-pack:end;box-pack:end;justify-content:flex-end;font-size:87%;padding-top:3px}@media print{.edit_mode div.cell.selected{border-color:transparent}div.code_cell{page-break-inside:avoid}#notebook-container{width:100%}.celltoolbar{display:none}}.ctb_hideshow{display:none;vertical-align:bottom}.ctb_global_show .ctb_show.ctb_hideshow{display:block}.ctb_global_show .ctb_show+.input_area,.ctb_global_show .ctb_show+div.text_cell_input,.ctb_global_show .ctb_show~div.text_cell_render{border-top-right-radius:0;border-top-left-radius:0}.ctb_global_show .ctb_show~div.text_cell_render{border:1px solid #cfcfcf}.celltoolbar select{color:#555;background-color:#fff;background-image:none;border:1px solid #ccc;-webkit-box-shadow:inset 0 1px 1px rgba(0,0,0,.075);box-shadow:inset 0 1px 1px rgba(0,0,0,.075);-webkit-transition:border-color ease-in-out .15s,box-shadow ease-in-out .15s;-o-transition:border-color ease-in-out .15s,box-shadow ease-in-out .15s;transition:border-color ease-in-out .15s,box-shadow ease-in-out .15s;line-height:1.5;border-radius:1px;width:inherit;font-size:inherit;height:22px;padding:0;display:inline-block}.celltoolbar select:focus{border-color:#66afe9;outline:0;-webkit-box-shadow:inset 0 1px 1px rgba(0,0,0,.075),0 0 8px rgba(102,175,233,.6);box-shadow:inset 0 1px 1px rgba(0,0,0,.075),0 0 8px rgba(102,175,233,.6)}.celltoolbar select::-moz-placeholder{color:#999;opacity:1}.celltoolbar select:-ms-input-placeholder{color:#999}.celltoolbar select::-webkit-input-placeholder{color:#999}.celltoolbar select[disabled],.celltoolbar select[readonly],fieldset[disabled] .celltoolbar select{background-color:#eee;opacity:1}.celltoolbar select[disabled],fieldset[disabled] .celltoolbar select{cursor:not-allowed}textarea.celltoolbar select{height:auto}select.celltoolbar select{height:30px;line-height:30px}select[multiple].celltoolbar select,textarea.celltoolbar select{height:auto}.celltoolbar label{margin-left:5px;margin-right:5px}.completions{position:absolute;z-index:10;overflow:hidden;border:1px solid #ababab;border-radius:2px;-webkit-box-shadow:0 6px 10px -1px #adadad;box-shadow:0 6px 10px -1px #adadad;line-height:1}.completions select{background:#fff;outline:0;border:none;padding:0;margin:0;overflow:auto;font-family:monospace;font-size:110%;color:#000;width:auto}.completions select option.context{color:#286090}#kernel_logo_widget{float:right!important;float:right}#kernel_logo_widget .current_kernel_logo{display:none;margin-top:-1px;margin-bottom:-1px;width:32px;height:32px}#menubar{box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box;margin-top:1px}#menubar .navbar{border-top:1px;border-radius:0 0 2px 2px;margin-bottom:0}#menubar .navbar-toggle{float:left;padding-top:7px;padding-bottom:7px;border:none}#menubar .navbar-collapse{clear:left}.nav-wrapper{border-bottom:1px solid #e7e7e7}i.menu-icon{padding-top:4px}ul#help_menu li a{overflow:hidden;padding-right:2.2em}ul#help_menu li a i{margin-right:-1.2em}.dropdown-submenu{position:relative}.dropdown-submenu>.dropdown-menu{top:0;left:100%;margin-top:-6px;margin-left:-1px}.dropdown-submenu:hover>.dropdown-menu{display:block}.dropdown-submenu>a:after{font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;display:block;content:"\f0da";float:right;color:#333;margin-top:2px;margin-right:-10px}.dropdown-submenu>a:after.pull-left{margin-right:.3em}.dropdown-submenu>a:after.pull-right{margin-left:.3em}.dropdown-submenu:hover>a:after{color:#262626}.dropdown-submenu.pull-left{float:none}.dropdown-submenu.pull-left>.dropdown-menu{left:-100%;margin-left:10px}#notification_area{float:right!important;float:right;z-index:10}.indicator_area{float:right!important;float:right;color:#777;margin-left:5px;margin-right:5px;z-index:10;text-align:center;width:auto}#kernel_indicator{float:right!important;float:right;color:#777;margin-left:5px;margin-right:5px;z-index:10;text-align:center;width:auto;border-left:1px solid}#kernel_indicator .kernel_indicator_name{padding-left:5px;padding-right:5px}#modal_indicator{float:right!important;float:right;color:#777;margin-left:5px;margin-right:5px;z-index:10;text-align:center;width:auto}#readonly-indicator{float:right!important;float:right;color:#777;z-index:10;text-align:center;width:auto;display:none;margin:2px 0 0}.modal_indicator:before{width:1.28571429em;text-align:center}.edit_mode .modal_indicator:before{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;content:"\f040"}.edit_mode .modal_indicator:before.pull-left{margin-right:.3em}.edit_mode .modal_indicator:before.pull-right{margin-left:.3em}.command_mode .modal_indicator:before{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;content:' '}.command_mode .modal_indicator:before.pull-left{margin-right:.3em}.command_mode .modal_indicator:before.pull-right{margin-left:.3em}.kernel_idle_icon:before{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;content:"\f10c"}.kernel_idle_icon:before.pull-left{margin-right:.3em}.kernel_idle_icon:before.pull-right{margin-left:.3em}.kernel_busy_icon:before{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;content:"\f111"}.kernel_busy_icon:before.pull-left{margin-right:.3em}.kernel_busy_icon:before.pull-right{margin-left:.3em}.kernel_dead_icon:before{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;content:"\f1e2"}.kernel_dead_icon:before.pull-left{margin-right:.3em}.kernel_dead_icon:before.pull-right{margin-left:.3em}.kernel_disconnected_icon:before{display:inline-block;font:normal normal normal 14px/1 FontAwesome;font-size:inherit;text-rendering:auto;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;content:"\f127"}.kernel_disconnected_icon:before.pull-left{margin-right:.3em}.kernel_disconnected_icon:before.pull-right{margin-left:.3em}.notification_widget{z-index:10;background:rgba(240,240,240,.5);margin-right:4px;color:#333;background-color:#fff;border-color:#ccc}.notification_widget.active,.notification_widget.focus,.notification_widget:active,.notification_widget:focus,.notification_widget:hover,.open>.dropdown-toggle.notification_widget{color:#333;background-color:#e6e6e6;border-color:#adadad}.notification_widget.active,.notification_widget:active,.open>.dropdown-toggle.notification_widget{background-image:none}.notification_widget.disabled,.notification_widget.disabled.active,.notification_widget.disabled.focus,.notification_widget.disabled:active,.notification_widget.disabled:focus,.notification_widget.disabled:hover,.notification_widget[disabled],.notification_widget[disabled].active,.notification_widget[disabled].focus,.notification_widget[disabled]:active,.notification_widget[disabled]:focus,.notification_widget[disabled]:hover,fieldset[disabled] .notification_widget,fieldset[disabled] .notification_widget.active,fieldset[disabled] .notification_widget.focus,fieldset[disabled] .notification_widget:active,fieldset[disabled] .notification_widget:focus,fieldset[disabled] .notification_widget:hover{background-color:#fff;border-color:#ccc}.notification_widget .badge{color:#fff;background-color:#333}.notification_widget.warning{color:#fff;background-color:#f0ad4e;border-color:#eea236}.notification_widget.warning.active,.notification_widget.warning.focus,.notification_widget.warning:active,.notification_widget.warning:focus,.notification_widget.warning:hover,.open>.dropdown-toggle.notification_widget.warning{color:#fff;background-color:#ec971f;border-color:#d58512}.notification_widget.warning.active,.notification_widget.warning:active,.open>.dropdown-toggle.notification_widget.warning{background-image:none}.notification_widget.warning.disabled,.notification_widget.warning.disabled.active,.notification_widget.warning.disabled.focus,.notification_widget.warning.disabled:active,.notification_widget.warning.disabled:focus,.notification_widget.warning.disabled:hover,.notification_widget.warning[disabled],.notification_widget.warning[disabled].active,.notification_widget.warning[disabled].focus,.notification_widget.warning[disabled]:active,.notification_widget.warning[disabled]:focus,.notification_widget.warning[disabled]:hover,fieldset[disabled] .notification_widget.warning,fieldset[disabled] .notification_widget.warning.active,fieldset[disabled] .notification_widget.warning.focus,fieldset[disabled] .notification_widget.warning:active,fieldset[disabled] .notification_widget.warning:focus,fieldset[disabled] .notification_widget.warning:hover{background-color:#f0ad4e;border-color:#eea236}.notification_widget.warning .badge{color:#f0ad4e;background-color:#fff}.notification_widget.success{color:#fff;background-color:#5cb85c;border-color:#4cae4c}.notification_widget.success.active,.notification_widget.success.focus,.notification_widget.success:active,.notification_widget.success:focus,.notification_widget.success:hover,.open>.dropdown-toggle.notification_widget.success{color:#fff;background-color:#449d44;border-color:#398439}.notification_widget.success.active,.notification_widget.success:active,.open>.dropdown-toggle.notification_widget.success{background-image:none}.notification_widget.success.disabled,.notification_widget.success.disabled.active,.notification_widget.success.disabled.focus,.notification_widget.success.disabled:active,.notification_widget.success.disabled:focus,.notification_widget.success.disabled:hover,.notification_widget.success[disabled],.notification_widget.success[disabled].active,.notification_widget.success[disabled].focus,.notification_widget.success[disabled]:active,.notification_widget.success[disabled]:focus,.notification_widget.success[disabled]:hover,fieldset[disabled] .notification_widget.success,fieldset[disabled] .notification_widget.success.active,fieldset[disabled] .notification_widget.success.focus,fieldset[disabled] .notification_widget.success:active,fieldset[disabled] .notification_widget.success:focus,fieldset[disabled] .notification_widget.success:hover{background-color:#5cb85c;border-color:#4cae4c}.notification_widget.success .badge{color:#5cb85c;background-color:#fff}.notification_widget.info{color:#fff;background-color:#5bc0de;border-color:#46b8da}.notification_widget.info.active,.notification_widget.info.focus,.notification_widget.info:active,.notification_widget.info:focus,.notification_widget.info:hover,.open>.dropdown-toggle.notification_widget.info{color:#fff;background-color:#31b0d5;border-color:#269abc}.notification_widget.info.active,.notification_widget.info:active,.open>.dropdown-toggle.notification_widget.info{background-image:none}.notification_widget.info.disabled,.notification_widget.info.disabled.active,.notification_widget.info.disabled.focus,.notification_widget.info.disabled:active,.notification_widget.info.disabled:focus,.notification_widget.info.disabled:hover,.notification_widget.info[disabled],.notification_widget.info[disabled].active,.notification_widget.info[disabled].focus,.notification_widget.info[disabled]:active,.notification_widget.info[disabled]:focus,.notification_widget.info[disabled]:hover,fieldset[disabled] .notification_widget.info,fieldset[disabled] .notification_widget.info.active,fieldset[disabled] .notification_widget.info.focus,fieldset[disabled] .notification_widget.info:active,fieldset[disabled] .notification_widget.info:focus,fieldset[disabled] .notification_widget.info:hover{background-color:#5bc0de;border-color:#46b8da}.notification_widget.info .badge{color:#5bc0de;background-color:#fff}.notification_widget.danger{color:#fff;background-color:#d9534f;border-color:#d43f3a}.notification_widget.danger.active,.notification_widget.danger.focus,.notification_widget.danger:active,.notification_widget.danger:focus,.notification_widget.danger:hover,.open>.dropdown-toggle.notification_widget.danger{color:#fff;background-color:#c9302c;border-color:#ac2925}.notification_widget.danger.active,.notification_widget.danger:active,.open>.dropdown-toggle.notification_widget.danger{background-image:none}.notification_widget.danger.disabled,.notification_widget.danger.disabled.active,.notification_widget.danger.disabled.focus,.notification_widget.danger.disabled:active,.notification_widget.danger.disabled:focus,.notification_widget.danger.disabled:hover,.notification_widget.danger[disabled],.notification_widget.danger[disabled].active,.notification_widget.danger[disabled].focus,.notification_widget.danger[disabled]:active,.notification_widget.danger[disabled]:focus,.notification_widget.danger[disabled]:hover,fieldset[disabled] .notification_widget.danger,fieldset[disabled] .notification_widget.danger.active,fieldset[disabled] .notification_widget.danger.focus,fieldset[disabled] .notification_widget.danger:active,fieldset[disabled] .notification_widget.danger:focus,fieldset[disabled] .notification_widget.danger:hover{background-color:#d9534f;border-color:#d43f3a}.notification_widget.danger .badge{color:#d9534f;background-color:#fff}div#pager{background-color:#fff;font-size:14px;line-height:20px;overflow:hidden;display:none;position:fixed;bottom:0;width:100%;max-height:50%;padding-top:8px;-webkit-box-shadow:0 0 12px 1px rgba(87,87,87,.2);box-shadow:0 0 12px 1px rgba(87,87,87,.2);z-index:100;top:auto!important}div#pager pre{line-height:1.21429em;color:#000;background-color:#f7f7f7;padding:.4em}div#pager #pager-button-area{position:absolute;top:8px;right:20px}div#pager #pager-contents{position:relative;overflow:auto;width:100%;height:100%}div#pager #pager-contents #pager-container{position:relative;padding:15px 0;box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box}div#pager .ui-resizable-handle{top:0;height:8px;background:#f7f7f7;border-top:1px solid #cfcfcf;border-bottom:1px solid #cfcfcf}div#pager .ui-resizable-handle::after{content:'';top:2px;left:50%;height:3px;width:30px;margin-left:-15px;position:absolute;border-top:1px solid #cfcfcf}.quickhelp{display:-webkit-box;-webkit-box-orient:horizontal;display:-moz-box;-moz-box-orient:horizontal;display:box;box-orient:horizontal;box-align:stretch;display:flex;flex-direction:row;align-items:stretch}.shortcut_key{display:inline-block;width:20ex;text-align:right;font-family:monospace}.shortcut_descr{display:inline-block;-webkit-box-flex:1;-moz-box-flex:1;box-flex:1;flex:1}span.save_widget{margin-top:6px}span.save_widget span.filename{height:1em;line-height:1em;padding:3px;margin-left:16px;border:none;font-size:146.5%;border-radius:2px}span.save_widget span.filename:hover{background-color:#e6e6e6}span.autosave_status,span.checkpoint_status{font-size:small}@media (max-width:767px){span.save_widget{font-size:small}span.autosave_status,span.checkpoint_status{display:none}}@media (min-width:768px)and (max-width:991px){span.checkpoint_status{display:none}span.autosave_status{font-size:x-small}}.toolbar{padding:0;margin-left:-5px;margin-top:2px;margin-bottom:5px;box-sizing:border-box;-moz-box-sizing:border-box;-webkit-box-sizing:border-box}.toolbar label,.toolbar select{width:auto;vertical-align:middle;margin-bottom:0;display:inline;font-size:92%;margin-left:.3em;margin-right:.3em;padding:3px 0 0}.toolbar .btn{padding:2px 8px}.toolbar .btn-group{margin-top:0;margin-left:5px}#maintoolbar{margin-bottom:-3px;margin-top:-8px;border:0;min-height:27px;margin-left:0;padding-top:11px;padding-bottom:3px}#maintoolbar .navbar-text{float:none;vertical-align:middle;text-align:right;margin-left:5px;margin-right:0;margin-top:0}.select-xs{height:24px}@-moz-keyframes fadeOut{from{opacity:1}to{opacity:0}}@-webkit-keyframes fadeOut{from{opacity:1}to{opacity:0}}@-moz-keyframes fadeIn{from{opacity:0}to{opacity:1}}@-webkit-keyframes fadeIn{from{opacity:0}to{opacity:1}}.bigtooltip{overflow:auto;height:200px;-webkit-transition-property:height;-webkit-transition-duration:500ms;-moz-transition-property:height;-moz-transition-duration:500ms;transition-property:height;transition-duration:500ms}.smalltooltip{-webkit-transition-property:height;-webkit-transition-duration:500ms;-moz-transition-property:height;-moz-transition-duration:500ms;transition-property:height;transition-duration:500ms;text-overflow:ellipsis;overflow:hidden;height:80px}.tooltipbuttons{position:absolute;padding-right:15px;top:0;right:0}.tooltiptext{padding-right:30px}.ipython_tooltip{max-width:700px;animation:fadeOut 400ms;-webkit-animation:fadeIn 400ms;-moz-animation:fadeIn 400ms;animation:fadeIn 400ms;vertical-align:middle;background-color:#f7f7f7;overflow:visible;border:1px solid #ababab;outline:0;padding:3px 3px 3px 7px;padding-left:7px;font-family:monospace;min-height:50px;-moz-box-shadow:0 6px 10px -1px #adadad;-webkit-box-shadow:0 6px 10px -1px #adadad;box-shadow:0 6px 10px -1px #adadad;border-radius:2px;position:absolute;z-index:1000}.ipython_tooltip a{float:right}.ipython_tooltip .tooltiptext pre{border:0;border-radius:0;font-size:100%;background-color:#f7f7f7}.pretooltiparrow{left:0;margin:0;top:-16px;width:40px;height:16px;overflow:hidden;position:absolute}.pretooltiparrow:before{background-color:#f7f7f7;border:1px solid #ababab;z-index:11;content:"";position:absolute;left:15px;top:10px;width:25px;height:25px;-webkit-transform:rotate(45deg);-moz-transform:rotate(45deg);-ms-transform:rotate(45deg);-o-transform:rotate(45deg)}.terminal-app{background:#eee}.terminal-app #header{background:#fff;-webkit-box-shadow:0 0 12px 1px rgba(87,87,87,.2);box-shadow:0 0 12px 1px rgba(87,87,87,.2)}.terminal-app .terminal{float:left;font-family:monospace;color:#fff;background:#000;padding:.4em;border-radius:2px;-webkit-box-shadow:0 0 12px 1px rgba(87,87,87,.4);box-shadow:0 0 12px 1px rgba(87,87,87,.4)}.terminal-app .terminal,.terminal-app .terminal dummy-screen{line-height:1em;font-size:14px}.terminal-app .terminal-cursor{color:#000;background:#fff}.terminal-app #terminado-container{margin-top:20px}
/*# sourceMappingURL=style.min.css.map */
    </style>
<style type="text/css">
    .highlight .hll { background-color: #ffffcc }
.highlight  { background: #f8f8f8; }
.highlight .c { color: #408080; font-style: italic } /* Comment */
.highlight .err { border: 1px solid #FF0000 } /* Error */
.highlight .k { color: #008000; font-weight: bold } /* Keyword */
.highlight .o { color: #666666 } /* Operator */
.highlight .ch { color: #408080; font-style: italic } /* Comment.Hashbang */
.highlight .cm { color: #408080; font-style: italic } /* Comment.Multiline */
.highlight .cp { color: #BC7A00 } /* Comment.Preproc */
.highlight .cpf { color: #408080; font-style: italic } /* Comment.PreprocFile */
.highlight .c1 { color: #408080; font-style: italic } /* Comment.Single */
.highlight .cs { color: #408080; font-style: italic } /* Comment.Special */
.highlight .gd { color: #A00000 } /* Generic.Deleted */
.highlight .ge { font-style: italic } /* Generic.Emph */
.highlight .gr { color: #FF0000 } /* Generic.Error */
.highlight .gh { color: #000080; font-weight: bold } /* Generic.Heading */
.highlight .gi { color: #00A000 } /* Generic.Inserted */
.highlight .go { color: #888888 } /* Generic.Output */
.highlight .gp { color: #000080; font-weight: bold } /* Generic.Prompt */
.highlight .gs { font-weight: bold } /* Generic.Strong */
.highlight .gu { color: #800080; font-weight: bold } /* Generic.Subheading */
.highlight .gt { color: #0044DD } /* Generic.Traceback */
.highlight .kc { color: #008000; font-weight: bold } /* Keyword.Constant */
.highlight .kd { color: #008000; font-weight: bold } /* Keyword.Declaration */
.highlight .kn { color: #008000; font-weight: bold } /* Keyword.Namespace */
.highlight .kp { color: #008000 } /* Keyword.Pseudo */
.highlight .kr { color: #008000; font-weight: bold } /* Keyword.Reserved */
.highlight .kt { color: #B00040 } /* Keyword.Type */
.highlight .m { color: #666666 } /* Literal.Number */
.highlight .s { color: #BA2121 } /* Literal.String */
.highlight .na { color: #7D9029 } /* Name.Attribute */
.highlight .nb { color: #008000 } /* Name.Builtin */
.highlight .nc { color: #0000FF; font-weight: bold } /* Name.Class */
.highlight .no { color: #880000 } /* Name.Constant */
.highlight .nd { color: #AA22FF } /* Name.Decorator */
.highlight .ni { color: #999999; font-weight: bold } /* Name.Entity */
.highlight .ne { color: #D2413A; font-weight: bold } /* Name.Exception */
.highlight .nf { color: #0000FF } /* Name.Function */
.highlight .nl { color: #A0A000 } /* Name.Label */
.highlight .nn { color: #0000FF; font-weight: bold } /* Name.Namespace */
.highlight .nt { color: #008000; font-weight: bold } /* Name.Tag */
.highlight .nv { color: #19177C } /* Name.Variable */
.highlight .ow { color: #AA22FF; font-weight: bold } /* Operator.Word */
.highlight .w { color: #bbbbbb } /* Text.Whitespace */
.highlight .mb { color: #666666 } /* Literal.Number.Bin */
.highlight .mf { color: #666666 } /* Literal.Number.Float */
.highlight .mh { color: #666666 } /* Literal.Number.Hex */
.highlight .mi { color: #666666 } /* Literal.Number.Integer */
.highlight .mo { color: #666666 } /* Literal.Number.Oct */
.highlight .sb { color: #BA2121 } /* Literal.String.Backtick */
.highlight .sc { color: #BA2121 } /* Literal.String.Char */
.highlight .sd { color: #BA2121; font-style: italic } /* Literal.String.Doc */
.highlight .s2 { color: #BA2121 } /* Literal.String.Double */
.highlight .se { color: #BB6622; font-weight: bold } /* Literal.String.Escape */
.highlight .sh { color: #BA2121 } /* Literal.String.Heredoc */
.highlight .si { color: #BB6688; font-weight: bold } /* Literal.String.Interpol */
.highlight .sx { color: #008000 } /* Literal.String.Other */
.highlight .sr { color: #BB6688 } /* Literal.String.Regex */
.highlight .s1 { color: #BA2121 } /* Literal.String.Single */
.highlight .ss { color: #19177C } /* Literal.String.Symbol */
.highlight .bp { color: #008000 } /* Name.Builtin.Pseudo */
.highlight .vc { color: #19177C } /* Name.Variable.Class */
.highlight .vg { color: #19177C } /* Name.Variable.Global */
.highlight .vi { color: #19177C } /* Name.Variable.Instance */
.highlight .il { color: #666666 } /* Literal.Number.Integer.Long */
    </style>


<style type="text/css">
/* Overrides of notebook CSS for static HTML export */
body {
  overflow: visible;
  padding: 8px;
}

div#notebook {
  overflow: visible;
  border-top: none;
}

@media print {
  div.cell {
    display: block;
    page-break-inside: avoid;
  } 
  div.output_wrapper { 
    display: block;
    page-break-inside: avoid; 
  }
  div.output { 
    display: block;
    page-break-inside: avoid; 
  }
}
</style>

<!-- Custom stylesheet, it must be in the same directory as the html file -->
<link rel="stylesheet" href="custom.css">

<!-- Loading mathjax macro -->
<!-- Load mathjax -->
    <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML"></script>
    <!-- MathJax configuration -->
    <script type="text/x-mathjax-config">
    MathJax.Hub.Config({
        tex2jax: {
            inlineMath: [ ['$','$'], ["\\(","\\)"] ],
            displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
            processEscapes: true,
            processEnvironments: true
        },
        // Center justify equations in code and markdown cells. Elsewhere
        // we use CSS to left justify single line equations in code cells.
        displayAlign: 'center',
        "HTML-CSS": {
            styles: {'.MathJax_Display': {"margin": 0}},
            linebreaks: { automatic: true }
        }
    });
    </script>
    <!-- End of mathjax configuration --></head>
<body>
  <div tabindex="-1" id="notebook" class="border-box-sizing">
    <div class="container" id="notebook-container">

<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[1]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="kn">import</span> <span class="nn">json</span>
<span class="kn">import</span> <span class="nn">pandas</span> <span class="kn">as</span> <span class="nn">pd</span>
<span class="kn">import</span> <span class="nn">matplotlib</span> <span class="kn">as</span> <span class="nn">plt</span>
<span class="kn">import</span> <span class="nn">scipy.spatial.distance</span> <span class="kn">as</span> <span class="nn">spdist</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="kn">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="kn">as</span> <span class="nn">sns</span>

<span class="o">%</span><span class="k">pylab</span> inline
<span class="n">sns</span><span class="o">.</span><span class="n">set_context</span><span class="p">(</span><span class="s1">&#39;poster&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>Populating the interactive namespace from numpy and matplotlib
</pre>
</div>
</div>

<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stderr output_text">
<pre>WARNING: pylab import has clobbered these variables: [&apos;plt&apos;]
&#96;%matplotlib&#96; prevents importing * from pylab and numpy
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[2]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="n">longitude</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">([</span><span class="o">-</span><span class="mf">0.0000000400893815</span><span class="p">,</span><span class="o">-</span><span class="mf">28.8732862244731230</span><span class="p">,</span><span class="o">-</span><span class="mf">79.2915791686897506</span><span class="p">,</span>
<span class="o">-</span><span class="mf">14.6577381710829471</span><span class="p">,</span><span class="o">-</span><span class="mf">64.7472605264735108</span><span class="p">,</span><span class="o">-</span><span class="mf">29.0584693142401171</span><span class="p">,</span><span class="o">-</span><span class="mf">72.0785319657452987</span><span class="p">,</span>
<span class="o">-</span><span class="mf">36.0366489745023770</span><span class="p">,</span><span class="o">-</span><span class="mf">50.4808382862985496</span><span class="p">,</span><span class="o">-</span><span class="mf">50.5859026832315024</span><span class="p">,</span> <span class="o">-</span><span class="mf">0.1358203773809326</span><span class="p">,</span>
<span class="o">-</span><span class="mf">65.0865638413727368</span><span class="p">,</span><span class="o">-</span><span class="mf">21.4983260706612533</span><span class="p">,</span><span class="o">-</span><span class="mf">57.5687244704708050</span><span class="p">,</span><span class="o">-</span><span class="mf">43.0700258454450875</span><span class="p">])</span>

<span class="n">lattitude</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">([</span><span class="mf">0.0000000358808126</span><span class="p">,</span><span class="o">-</span><span class="mf">0.0000008724121069</span><span class="p">,</span><span class="mf">21.4033307581457670</span><span class="p">,</span>
 <span class="mf">43.3895496964974043</span><span class="p">,</span><span class="o">-</span><span class="mf">21.8981713360336698</span><span class="p">,</span><span class="mf">43.2167287683090606</span><span class="p">,</span><span class="o">-</span><span class="mf">0.1815834632498404</span><span class="p">,</span>
 <span class="mf">21.6135482886620949</span><span class="p">,</span><span class="o">-</span><span class="mf">7.3744722432402208</span><span class="p">,</span><span class="mf">21.5881966132975371</span><span class="p">,</span><span class="mf">28.7292896751977480</span><span class="p">,</span>
 <span class="mf">36.0624693073746769</span><span class="p">,</span><span class="o">-</span><span class="mf">7.3194159498090388</span><span class="p">,</span><span class="mf">43.2505562436354225</span><span class="p">,</span><span class="o">-</span><span class="mf">14.5548396888330487</span><span class="p">])</span>

<span class="n">longitude</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">round</span><span class="p">(</span><span class="n">longitude</span><span class="p">)</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">)</span>
<span class="n">lattitude</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">round</span><span class="p">(</span><span class="n">lattitude</span><span class="p">)</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">int</span><span class="p">)</span>
<span class="n">longitude</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[2]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>array([  0, -29, -79, -15, -65, -29, -72, -36, -50, -51,   0, -65, -21,
       -58, -43])</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[3]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="n">coords</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">({</span><span class="s1">&#39;longitude&#39;</span><span class="p">:</span> <span class="n">longitude</span><span class="p">,</span> <span class="s1">&#39;lattitude&#39;</span><span class="p">:</span> <span class="n">lattitude</span><span class="p">})</span>
<span class="n">xticks</span> <span class="o">=</span> <span class="p">[</span><span class="n">label</span> <span class="k">for</span> <span class="n">label</span> <span class="ow">in</span> <span class="nb">xrange</span><span class="p">(</span><span class="o">-</span><span class="mi">90</span><span class="p">,</span> <span class="mi">10</span><span class="p">,</span> <span class="mi">10</span><span class="p">)]</span>
<span class="n">yticks</span> <span class="o">=</span> <span class="p">[</span><span class="n">label</span> <span class="k">for</span> <span class="n">label</span> <span class="ow">in</span> <span class="nb">xrange</span><span class="p">(</span><span class="o">-</span><span class="mi">20</span><span class="p">,</span> <span class="mi">50</span><span class="p">,</span> <span class="mi">10</span><span class="p">)]</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[4]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="n">distance</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span> <span class="p">(</span> <span class="n">np</span><span class="o">.</span><span class="n">round</span><span class="p">(</span><span class="n">spdist</span><span class="o">.</span><span class="n">cdist</span><span class="p">(</span> <span class="n">coords</span><span class="p">,</span> <span class="n">coords</span> <span class="p">),</span> <span class="n">decimals</span><span class="o">=</span><span class="mi">3</span> <span class="p">)</span> <span class="p">)</span> <span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[5]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="n">distance</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[5]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>10</th>
      <th>11</th>
      <th>12</th>
      <th>13</th>
      <th>14</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.000</td>
      <td>29.000</td>
      <td>81.744</td>
      <td>45.541</td>
      <td>68.622</td>
      <td>51.865</td>
      <td>72.000</td>
      <td>42.190</td>
      <td>50.488</td>
      <td>55.543</td>
      <td>29.000</td>
      <td>74.303</td>
      <td>22.136</td>
      <td>72.201</td>
      <td>45.541</td>
    </tr>
    <tr>
      <th>1</th>
      <td>29.000</td>
      <td>0.000</td>
      <td>54.231</td>
      <td>45.222</td>
      <td>42.190</td>
      <td>43.000</td>
      <td>43.000</td>
      <td>23.087</td>
      <td>22.136</td>
      <td>31.113</td>
      <td>41.012</td>
      <td>50.912</td>
      <td>10.630</td>
      <td>51.865</td>
      <td>20.518</td>
    </tr>
    <tr>
      <th>2</th>
      <td>81.744</td>
      <td>54.231</td>
      <td>0.000</td>
      <td>67.676</td>
      <td>45.222</td>
      <td>54.626</td>
      <td>22.136</td>
      <td>43.012</td>
      <td>40.311</td>
      <td>28.018</td>
      <td>79.404</td>
      <td>20.518</td>
      <td>64.405</td>
      <td>30.414</td>
      <td>50.912</td>
    </tr>
    <tr>
      <th>3</th>
      <td>45.541</td>
      <td>45.222</td>
      <td>67.676</td>
      <td>0.000</td>
      <td>82.006</td>
      <td>14.000</td>
      <td>71.400</td>
      <td>29.698</td>
      <td>61.033</td>
      <td>41.677</td>
      <td>20.518</td>
      <td>50.488</td>
      <td>50.359</td>
      <td>43.000</td>
      <td>64.405</td>
    </tr>
    <tr>
      <th>4</th>
      <td>68.622</td>
      <td>42.190</td>
      <td>45.222</td>
      <td>82.006</td>
      <td>0.000</td>
      <td>74.303</td>
      <td>23.087</td>
      <td>52.697</td>
      <td>21.213</td>
      <td>46.174</td>
      <td>82.620</td>
      <td>58.000</td>
      <td>46.487</td>
      <td>65.376</td>
      <td>23.087</td>
    </tr>
    <tr>
      <th>5</th>
      <td>51.865</td>
      <td>43.000</td>
      <td>54.626</td>
      <td>14.000</td>
      <td>74.303</td>
      <td>0.000</td>
      <td>60.811</td>
      <td>22.136</td>
      <td>54.231</td>
      <td>30.414</td>
      <td>32.202</td>
      <td>36.674</td>
      <td>50.636</td>
      <td>29.000</td>
      <td>59.666</td>
    </tr>
    <tr>
      <th>6</th>
      <td>72.000</td>
      <td>43.000</td>
      <td>22.136</td>
      <td>71.400</td>
      <td>23.087</td>
      <td>60.811</td>
      <td>0.000</td>
      <td>42.190</td>
      <td>23.087</td>
      <td>30.414</td>
      <td>77.621</td>
      <td>36.674</td>
      <td>51.478</td>
      <td>45.222</td>
      <td>32.650</td>
    </tr>
    <tr>
      <th>7</th>
      <td>42.190</td>
      <td>23.087</td>
      <td>43.012</td>
      <td>29.698</td>
      <td>52.697</td>
      <td>22.136</td>
      <td>42.190</td>
      <td>0.000</td>
      <td>32.202</td>
      <td>15.000</td>
      <td>36.674</td>
      <td>32.202</td>
      <td>32.650</td>
      <td>30.414</td>
      <td>37.656</td>
    </tr>
    <tr>
      <th>8</th>
      <td>50.488</td>
      <td>22.136</td>
      <td>40.311</td>
      <td>61.033</td>
      <td>21.213</td>
      <td>54.231</td>
      <td>23.087</td>
      <td>32.202</td>
      <td>0.000</td>
      <td>29.017</td>
      <td>61.612</td>
      <td>45.541</td>
      <td>29.000</td>
      <td>50.636</td>
      <td>10.630</td>
    </tr>
    <tr>
      <th>9</th>
      <td>55.543</td>
      <td>31.113</td>
      <td>28.018</td>
      <td>41.677</td>
      <td>46.174</td>
      <td>30.414</td>
      <td>30.414</td>
      <td>15.000</td>
      <td>29.017</td>
      <td>0.000</td>
      <td>51.478</td>
      <td>19.799</td>
      <td>41.725</td>
      <td>22.136</td>
      <td>37.855</td>
    </tr>
    <tr>
      <th>10</th>
      <td>29.000</td>
      <td>41.012</td>
      <td>79.404</td>
      <td>20.518</td>
      <td>82.620</td>
      <td>32.202</td>
      <td>77.621</td>
      <td>36.674</td>
      <td>61.612</td>
      <td>51.478</td>
      <td>0.000</td>
      <td>65.376</td>
      <td>41.677</td>
      <td>59.666</td>
      <td>61.522</td>
    </tr>
    <tr>
      <th>11</th>
      <td>74.303</td>
      <td>50.912</td>
      <td>20.518</td>
      <td>50.488</td>
      <td>58.000</td>
      <td>36.674</td>
      <td>36.674</td>
      <td>32.202</td>
      <td>45.541</td>
      <td>19.799</td>
      <td>65.376</td>
      <td>0.000</td>
      <td>61.522</td>
      <td>9.899</td>
      <td>55.543</td>
    </tr>
    <tr>
      <th>12</th>
      <td>22.136</td>
      <td>10.630</td>
      <td>64.405</td>
      <td>50.359</td>
      <td>46.487</td>
      <td>50.636</td>
      <td>51.478</td>
      <td>32.650</td>
      <td>29.000</td>
      <td>41.725</td>
      <td>41.677</td>
      <td>61.522</td>
      <td>0.000</td>
      <td>62.201</td>
      <td>23.409</td>
    </tr>
    <tr>
      <th>13</th>
      <td>72.201</td>
      <td>51.865</td>
      <td>30.414</td>
      <td>43.000</td>
      <td>65.376</td>
      <td>29.000</td>
      <td>45.222</td>
      <td>30.414</td>
      <td>50.636</td>
      <td>22.136</td>
      <td>59.666</td>
      <td>9.899</td>
      <td>62.201</td>
      <td>0.000</td>
      <td>59.908</td>
    </tr>
    <tr>
      <th>14</th>
      <td>45.541</td>
      <td>20.518</td>
      <td>50.912</td>
      <td>64.405</td>
      <td>23.087</td>
      <td>59.666</td>
      <td>32.650</td>
      <td>37.656</td>
      <td>10.630</td>
      <td>37.855</td>
      <td>61.522</td>
      <td>55.543</td>
      <td>23.409</td>
      <td>59.908</td>
      <td>0.000</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[11]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="k">def</span> <span class="nf">get_shortest_path</span><span class="p">(</span><span class="n">distance</span><span class="p">,</span> <span class="n">current_node</span><span class="p">):</span>
    <span class="n">total_nodes</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">distance</span><span class="o">.</span><span class="n">columns</span><span class="p">)</span> <span class="o">-</span> <span class="mi">1</span>
    <span class="n">sequence</span> <span class="o">=</span> <span class="p">[</span><span class="n">current_node</span><span class="p">]</span>
    <span class="n">a</span> <span class="o">=</span> <span class="n">distance</span><span class="o">.</span><span class="n">T</span>
    <span class="n">a</span> <span class="o">=</span> <span class="n">a</span><span class="o">.</span><span class="n">replace</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="n">np</span><span class="o">.</span><span class="n">nan</span><span class="p">)</span>
    <span class="n">a</span> <span class="o">=</span> <span class="n">a</span><span class="p">[</span><span class="n">a</span><span class="o">.</span><span class="n">index</span><span class="o">.</span><span class="n">values</span> <span class="o">!=</span> <span class="n">current_node</span><span class="p">]</span>

    <span class="k">while</span> <span class="n">total_nodes</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="p">:</span>
        <span class="n">current_node</span> <span class="o">=</span> <span class="n">a</span><span class="p">[</span><span class="n">current_node</span><span class="p">]</span><span class="o">.</span><span class="n">idxmin</span><span class="p">()</span>
        <span class="n">sequence</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">current_node</span><span class="p">)</span>
        <span class="c1">#a.drop(a.index[current_node], inplace=True)</span>
        <span class="n">a</span> <span class="o">=</span> <span class="n">a</span><span class="p">[</span><span class="n">a</span><span class="o">.</span><span class="n">index</span><span class="o">.</span><span class="n">values</span> <span class="o">!=</span> <span class="n">current_node</span><span class="p">]</span>
        <span class="n">total_nodes</span> <span class="o">-=</span> <span class="mi">1</span>
    <span class="k">return</span> <span class="n">sequence</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[41]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="n">origin</span> <span class="o">=</span> <span class="mi">7</span>
<span class="n">path</span> <span class="o">=</span> <span class="n">get_shortest_path</span><span class="p">(</span><span class="n">distance</span><span class="p">,</span> <span class="n">origin</span><span class="p">)</span>
<span class="n">path</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">origin</span><span class="p">)</span>
<span class="k">print</span> <span class="n">path</span>

<span class="c1"># size of scatter markers</span>
<span class="n">s</span> <span class="o">=</span> <span class="p">[</span><span class="mi">700</span> <span class="k">if</span> <span class="n">i</span> <span class="o">==</span> <span class="n">origin</span> <span class="k">else</span> <span class="mi">100</span> <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="n">coords</span><span class="o">.</span><span class="n">index</span><span class="o">.</span><span class="n">values</span><span class="p">]</span>

<span class="n">fig</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">()</span>
<span class="n">ax</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">coords</span><span class="o">.</span><span class="n">longitude</span><span class="p">,</span> <span class="n">coords</span><span class="o">.</span><span class="n">lattitude</span><span class="p">,</span> <span class="n">s</span><span class="o">=</span><span class="n">s</span><span class="p">)</span> 
<span class="n">plt</span><span class="o">.</span><span class="n">xticks</span><span class="p">(</span><span class="n">xticks</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">yticks</span><span class="p">(</span><span class="n">yticks</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;longitude&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;lattitude&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">axis</span><span class="p">(</span><span class="s1">&#39;equal&#39;</span><span class="p">)</span>
<span class="c1"># Set annotation for each point</span>
<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="n">coords</span><span class="o">.</span><span class="n">index</span><span class="o">.</span><span class="n">values</span><span class="p">:</span>
    <span class="n">ax</span><span class="o">.</span><span class="n">text</span><span class="p">(</span><span class="n">coords</span><span class="o">.</span><span class="n">longitude</span><span class="p">[</span><span class="n">i</span><span class="p">],</span> <span class="n">coords</span><span class="o">.</span><span class="n">lattitude</span><span class="p">[</span><span class="n">i</span><span class="p">],</span> <span class="nb">str</span><span class="p">(</span><span class="n">i</span><span class="p">),</span> <span class="n">verticalalignment</span><span class="o">=</span><span class="s1">&#39;bottom&#39;</span><span class="p">)</span>

<span class="n">i</span> <span class="o">=</span> <span class="mi">0</span>
<span class="k">while</span> <span class="n">i</span> <span class="o">&lt;</span> <span class="nb">len</span><span class="p">(</span><span class="n">path</span><span class="p">)</span> <span class="o">-</span> <span class="mi">1</span><span class="p">:</span>
    <span class="n">first</span> <span class="o">=</span> <span class="n">path</span><span class="p">[</span><span class="n">i</span><span class="p">]</span>
    <span class="n">second</span> <span class="o">=</span> <span class="n">path</span><span class="p">[</span><span class="n">i</span><span class="o">+</span><span class="mi">1</span><span class="p">]</span>
    <span class="n">coord_x</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="n">coords</span><span class="o">.</span><span class="n">loc</span><span class="p">[[</span><span class="n">first</span><span class="p">,</span> <span class="n">second</span><span class="p">],</span> <span class="s1">&#39;longitude&#39;</span><span class="p">])</span>
    <span class="n">coord_y</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="n">coords</span><span class="o">.</span><span class="n">loc</span><span class="p">[[</span><span class="n">first</span><span class="p">,</span> <span class="n">second</span><span class="p">],</span> <span class="s1">&#39;lattitude&#39;</span><span class="p">])</span>
    <span class="n">i</span> <span class="o">+=</span> <span class="mi">1</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">coord_x</span><span class="p">,</span> <span class="n">coord_y</span><span class="p">,</span> <span class="s1">&#39;r&#39;</span><span class="p">)</span>
    <span class="c1">#plt.arrow(coord_x[0], coord_x[1], coord_y[0], coord_y[1], shape=&#39;full&#39;, lw=3, length_includes_head=True, head_width=.01)</span>
    <span class="c1">#plt.arrow</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>[7, 9, 11, 13, 5, 3, 10, 0, 12, 1, 14, 8, 4, 6, 2, 7]
</pre>
</div>
</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAxUAAAIqCAYAAABSRmfGAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz
AAALEgAACxIB0t1+/AAAIABJREFUeJzs3Xl4VOX9v/F7skKAJAi4gSAqnFZFa60VW63ihktFxaXu
UsG1btVqrXxFK1YtVlvXKnX9aVVaFUVccNdq69baKipHdhTZMSEQss78/pgkJiRAQiaZSeZ+XVeu
MOecnPnkccw173m2SCwWQ5IkSZI2VUayC5AkSZLUsRkqJEmSJLWKoUKSJElSqxgqJEmSJLWKoUKS
JElSqxgqJEmSJLVKVrILSEXLlpVsdJ3dwsI8AIqKStu8no7CNmnI9mjMNmnMNmnI9mjMNmnMNmnI
9mjMNmk7ffr0iDR13J4KSZIkSa1iqJAkSZLUKoYKSZIkSa1iqJAkSZLUKk7UltRhffrpdM47bzR3
3DGRIUN2bXDuX/96m4cffpA5c2aRlZXF7rvvwZlnnke/ftskqVqp7f3f//2aN998rdHxSCTCnXf+
pdH/J0qsefPmMnHiXXz66cesXVtGEHyH0077OXvsMTTZpUltzlAhqUNauPArxo69jFis8WJtL730
IuPHX8Xgwd/hzDPPY82a1fztb4/x/vunc++9/4++ffsloWKp7c2ePZNBgwZz4omnsu7/Gv37D0hO
UWli/vx5nHXWKLp27cqxx55IXl5Xpk59hksuuYDf/vYG9t//wGSXKLUpQ4WkDuedd/7BDTf8llWr
VjU6V1VVxa233kT//gO4++77yc7OBmDo0B8xevSpPPjgvYwde007Vyy1vbKyMr7+eiEjRx7PQQcd
kuxy0s5dd91KVVUVt99+T12AO/TQIzj55GP5859vM1So03NOhaQO5ZprxnLFFZfQs+dmHHDAwY3O
L1mymB12GMzRRx9bFygABg/+DgUFBcyc+UV7liu1mzlzZhGNRtluu+2TXUpaysnJZf/9D2zQI5SX
l8dOOw1hyZLFlJSUJLE6qe3ZUyGpQ1mwYB5jxpzDSSedxsMPP9DofN++/bj11j83Or548SKKi4sZ
MuR77VGm1O5mzZpJJBJh4MDtgHjPRW5uLpFIk/tUKcHGj7+x0bHq6mpmz55J9+496NGjRxKqktqP
oUJShzJx4kNkZTX/T9fy5cv4/PNPueeeO+nSpQujRo1pw+qk5Jk1K94L98or0/i///s1K1Ysp0uX
LvzkJ8O44IJLKCwsTHKF6WPVqlXMmzeHRx55kIULv+KXv7w82SVJbc5QIalDaUmgqKysZOTIw+se
n3XWeQweHLRFWVLSzZ49C4AZMz7nnHPOp2vXPD788H2mTHmKGTM+4y9/eYi8vG5JrjI9/PrXFzN9
+idEIhH22WdfDj30p8kuSWpzhgpJnVZVVRXXXnsD1dVRXn31Je65507mzJnNuHHjk12alHCHHXYE
e+65F6ecMoqMjPiUyX33HUb//gO47babeeyxRxg9+uwkV5keTj55FAAfffRvnnxyEmeeeRp//vP9
dO/ePbmFSW3IidqSOq2uXbuy334HcMABB3H99Tex//4H8sor0/jf/z5KdmlSwh1++AhOO+2MukBR
6+ijjyUzM5MPPngvSZWln733/gl77/0TLrjgl1x88a+YN28uTzzxeLLLktqUoUJS2jjooEOJxWLM
mPFZskuR2k1WVhbdu/egtHRNsktJSwcffCiAf3fU6RkqJHUqr7/+CiNHHs7LL7/Y6Fztm6rc3Nz2
LktqU0uXLuG0037G9df/ttG5oqIiiouL6NevfxIqSw+LFy/ihBNGcvPNv290rrS0FPDvjjo/Q4Wk
lBaGM3j++Zd5//33qK6u3uj1228/iOXLl/G3vz1KVVVV3fGKigoef/wRsrOz2WuvvduyZKldzJkz
m+eff5m3336HgoJCSktLee21l1mwYH6D6+65504ikQiHHeZk4UT6+uuFvPTSq7z55lvk5XWjsrKC
l19+kcWLFze47sEH7yMSifCTn+yfpEql9uFEbUkp6dln3+Duu99mxoxdKSkZTHb2cnbYYQKHHbYV
l19++nrX3u/ffwAnn3w6f/3rQ5x33hiGDz+UsrIyXnhhKgsWzOfiiy9jiy22bOffRkqcd975kJtu
eoEZM77DypW7kJGxih12uI0hQ4awfPlrnHfeGI455njy8wt4++03+fe/P+CQQw5n7733TXbpncKM
GTMZN24Sn33Wn6VL9wDKGTjwfoIgYMWKdzj33DMYOfI48vK68c47b/Hhh+8zbNiBHHDAQckuXWpT
hgpJKeexx57j2mvLWLHi26EElZXw+eeHMHfuh3z99S3ceuul6/35s8/+BQMGbMsTT0zirrtuIysr
i+9+dycuuuhX7LHHnu3xK0ht4rXX/sUvf/kxixb9HogH62gUvvhif2bPnsXee6+hf/8YkyY9SmVl
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
gDZtmjJq1CgyM7OcLk9EREQSjEKFSAJr2LAho0cP3f+OIiIiIjWgaypERERERKRGFCpERERERKRG
FCpERERERKRGFCpERERERKRGFCpERERERKRGFCpERERERKRGFCpERERERKRGFCpERERERKRGFCpE
RERERKRGFCpERERERKRGFCpERERERKRGFCpERERERKRGFCpERERERKRGFCpERERERKRGFCpERERE
RKRGFCpERERERKRGXOFw2OkaREREREQkjulIhYiIiIiI1IhChYiIiIiI1IhChYiIiIiI1IhChYiI
iIiI1IhChYiIiIiI1IhChYiIiIiI1IhChYiIiIiI1IhChYiIiIiI1IhChYiIiIiI1IhChYiIiIiI
1IjH6QLijTHmImA8cASwGfi7ZVnPVtjnDOAh4FjgR+A+y7JeiHGpMWOMOQ14ADge2Am8BEy2LCtQ
Zp+k6YkxZhNw+F42T7Qs697IfsnUk0OAR4AB2B9mvA/cZlnWd2X2SZp+ABhj5mP3o6wwkGFZVlFk
n6TqSVnGmInYPy8pFdYnTU+MMX2BvwBdgJ+Axy3L+keFfZKmH1D69+avwIlAEbAUuN2yrJ/L7JNU
PQEwxmQAXwLjLMt6vcK2ZOzH1cDtwGHAGuy+fOxsVYlPRyoOgDFmFDAd+wd3EPAP4CFjzJ1l9jka
WARsBM4H5gPPGWOGxr7iumeM6QQsBvKAodhvHO8EJpfZJ6l6AgwBulf4NwvIB2ZAcvXEGOPB/sN/
MnAVMBroDCyMbEuqfpRxHPB3yr9OTi0TKJKxJwAYY34H/BE7ZJVdnzQ9McacCswDvsD+e/Ms8Igx
ZmyZfZKmH1D6fJcCucBI4A9AD+AtY4y7zD5J0xMAY0xjYC7QroptydiP0cBTwMvY70t2Yb9G9vZh
n9QSHak4MHcBKy3LGhVZftsY4wf+box51rKsXZF9NlmWdXFknyXGmBbAPcDrle8y7g3HDqcXWJa1
G1hqjGkL3AjcEdknqXpiWdbassvGmJOxf5mPsSzr28jqZOrJaOwje8ayrB8BjDFbgAXYn5x9TnL1
A2NMJvYbgLcsy/rvXnZLqp5EGWNSgOeAn4FDK2xOpp7cCnxpWdaYyPIyY0wX7N+tj0XWJVM/wH7u
PwHDLMsKAhhjNgD/BXoDb5FkPTHGnIX9BrrlXnZJqn5ETAKetizrrwDGmKWABdyG/XMldURHKg7M
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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[38]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="n">plt</span><span class="o">.</span><span class="n">arrow</span><span class="o">?</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[35]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="n">plt</span><span class="o">.</span><span class="n">arrow</span><span class="p">([</span><span class="mi">0</span><span class="p">,</span> <span class="mi">0</span><span class="p">],[</span><span class="mi">0</span><span class="p">,</span><span class="mi">1</span><span class="p">],</span> <span class="n">shape</span><span class="o">=</span><span class="s1">&#39;full&#39;</span><span class="p">,</span> <span class="n">lw</span><span class="o">=</span><span class="mi">3</span><span class="p">,</span> <span class="n">length_includes_head</span><span class="o">=</span><span class="bp">True</span><span class="p">,</span> <span class="n">head_width</span><span class="o">=.</span><span class="mo">01</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_text output_error">
<pre>
<span class="ansired">---------------------------------------------------------------------------</span>
<span class="ansired">TypeError</span>                                 Traceback (most recent call last)
<span class="ansigreen">&lt;ipython-input-35-302391a893f4&gt;</span> in <span class="ansicyan">&lt;module&gt;</span><span class="ansiblue">()</span>
<span class="ansigreen">----&gt; 1</span><span class="ansiyellow"> </span>plt<span class="ansiyellow">.</span>arrow<span class="ansiyellow">(</span><span class="ansiyellow">[</span><span class="ansicyan">0</span><span class="ansiyellow">,</span> <span class="ansicyan">0</span><span class="ansiyellow">]</span><span class="ansiyellow">,</span><span class="ansiyellow">[</span><span class="ansicyan">0</span><span class="ansiyellow">,</span><span class="ansicyan">1</span><span class="ansiyellow">]</span><span class="ansiyellow">,</span> shape<span class="ansiyellow">=</span><span class="ansiblue">&apos;full&apos;</span><span class="ansiyellow">,</span> lw<span class="ansiyellow">=</span><span class="ansicyan">3</span><span class="ansiyellow">,</span> length_includes_head<span class="ansiyellow">=</span>True<span class="ansiyellow">,</span> head_width<span class="ansiyellow">=</span><span class="ansicyan">.01</span><span class="ansiyellow">)</span><span class="ansiyellow"></span>

<span class="ansired">TypeError</span>: arrow() takes at least 4 arguments (2 given)</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre> 
</pre></div>

</div>
</div>
</div>

</div>
    </div>
  </div>
</body>
</html>
