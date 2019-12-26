cola Report for recount2:SRP056477
==================

**Date**: 2019-12-26 00:53:32 CET, **cola version**: 1.3.2

----------------------------------------------------------------

<style type='text/css'>

body, td, th {
   font-family: Arial,Helvetica,sans-serif;
   background-color: white;
   font-size: 13px;
  max-width: 800px;
  margin: auto;
  margin-left:210px;
  padding: 0px 10px 0px 10px;
  border-left: 1px solid #EEEEEE;
  line-height: 150%;
}

tt, code, pre {
   font-family: 'DejaVu Sans Mono', 'Droid Sans Mono', 'Lucida Console', Consolas, Monaco, 

monospace;
}

h1 {
   font-size:2.2em;
}

h2 {
   font-size:1.8em;
}

h3 {
   font-size:1.4em;
}

h4 {
   font-size:1.0em;
}

h5 {
   font-size:0.9em;
}

h6 {
   font-size:0.8em;
}

a {
  text-decoration: none;
  color: #0366d6;
}

a:hover {
  text-decoration: underline;
}

a:visited {
   color: #0366d6;
}

pre, img {
  max-width: 100%;
}
pre {
  overflow-x: auto;
}
pre code {
   display: block; padding: 0.5em;
}

code {
  font-size: 92%;
  border: 1px solid #ccc;
}

code[class] {
  background-color: #F8F8F8;
}

table, td, th {
  border: 1px solid #ccc;
}

blockquote {
   color:#666666;
   margin:0;
   padding-left: 1em;
   border-left: 0.5em #EEE solid;
}

hr {
   height: 0px;
   border-bottom: none;
   border-top-width: thin;
   border-top-style: dotted;
   border-top-color: #999999;
}

@media print {
   * {
      background: transparent !important;
      color: black !important;
      filter:none !important;
      -ms-filter: none !important;
   }

   body {
      font-size:12pt;
      max-width:100%;
   }

   a, a:visited {
      text-decoration: underline;
   }

   hr {
      visibility: hidden;
      page-break-before: always;
   }

   pre, blockquote {
      padding-right: 1em;
      page-break-inside: avoid;
   }

   tr, img {
      page-break-inside: avoid;
   }

   img {
      max-width: 100% !important;
   }

   @page :left {
      margin: 15mm 20mm 15mm 10mm;
   }

   @page :right {
      margin: 15mm 10mm 15mm 20mm;
   }

   p, h2, h3 {
      orphans: 3; widows: 3;
   }

   h2, h3 {
      page-break-after: avoid;
   }
}
</style>




## Summary





All available functions which can be applied to this `res_list` object:


```r
res_list
```

```
#> A 'ConsensusPartitionList' object with 24 methods.
#>   On a matrix with 16868 rows and 52 columns.
#>   Top rows are extracted by 'SD, CV, MAD, ATC' methods.
#>   Subgroups are detected by 'hclust, kmeans, skmeans, pam, mclust, NMF' method.
#>   Number of partitions are tried for k = 2, 3, 4, 5, 6.
#>   Performed in total 30000 partitions by row resampling.
#> 
#> Following methods can be applied to this 'ConsensusPartitionList' object:
#>  [1] "cola_report"           "collect_classes"       "collect_plots"         "collect_stats"        
#>  [5] "colnames"              "functional_enrichment" "get_anno_col"          "get_anno"             
#>  [9] "get_classes"           "get_matrix"            "get_membership"        "get_stats"            
#> [13] "is_best_k"             "is_stable_k"           "ncol"                  "nrow"                 
#> [17] "rownames"              "show"                  "suggest_best_k"        "test_to_known_factors"
#> [21] "top_rows_heatmap"      "top_rows_overlap"     
#> 
#> You can get result for a single method by, e.g. object["SD", "hclust"] or object["SD:hclust"]
#> or a subset of methods by object[c("SD", "CV")], c("hclust", "kmeans")]
```

The call of `run_all_consensus_partition_methods()` was:


```
#> run_all_consensus_partition_methods(data = mat, mc.cores = 4)
```

Dimension of the input matrix:


```r
mat = get_matrix(res_list)
dim(mat)
```

```
#> [1] 16868    52
```

### Density distribution

The density distribution for each sample is visualized as in one column in the
following heatmap. The clustering is based on the distance which is the
Kolmogorov-Smirnov statistic between two distributions.




```r
library(ComplexHeatmap)
densityHeatmap(mat, ylab = "value", cluster_columns = TRUE, show_column_names = FALSE,
    mc.cores = 4)
```

![plot of chunk density-heatmap](figure_cola/density-heatmap-1.png)





### Suggest the best k



Folowing table shows the best `k` (number of partitions) for each combination
of top-value methods and partition methods. Clicking on the method name in
the table goes to the section for a single combination of methods.

[The cola vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13)
explains the definition of the metrics used for determining the best
number of partitions.


```r
suggest_best_k(res_list)
```


|                            | The best k| 1-PAC| Mean silhouette| Concordance|   |Optional k |
|:---------------------------|----------:|-----:|---------------:|-----------:|:--|:----------|
|[SD:kmeans](#SD-kmeans)     |          2| 1.000|           1.000|       1.000|** |           |
|[SD:skmeans](#SD-skmeans)   |          5| 1.000|           0.980|       0.988|** |2,3,4      |
|[SD:NMF](#SD-NMF)           |          2| 1.000|           1.000|       1.000|** |           |
|[CV:kmeans](#CV-kmeans)     |          2| 1.000|           1.000|       1.000|** |           |
|[CV:skmeans](#CV-skmeans)   |          3| 1.000|           0.968|       0.978|** |2          |
|[CV:pam](#CV-pam)           |          2| 1.000|           0.991|       0.996|** |           |
|[CV:mclust](#CV-mclust)     |          2| 1.000|           1.000|       1.000|** |           |
|[CV:NMF](#CV-NMF)           |          2| 1.000|           1.000|       1.000|** |           |
|[MAD:kmeans](#MAD-kmeans)   |          2| 1.000|           1.000|       1.000|** |           |
|[MAD:skmeans](#MAD-skmeans) |          5| 1.000|           0.966|       0.982|** |2,3,4      |
|[MAD:NMF](#MAD-NMF)         |          2| 1.000|           1.000|       1.000|** |           |
|[ATC:kmeans](#ATC-kmeans)   |          2| 1.000|           1.000|       1.000|** |           |
|[ATC:mclust](#ATC-mclust)   |          6| 1.000|           0.971|       0.989|** |2,5        |
|[ATC:pam](#ATC-pam)         |          6| 0.984|           0.938|       0.973|** |2,3,4,5    |
|[SD:mclust](#SD-mclust)     |          5| 0.958|           0.883|       0.945|** |2,3        |
|[ATC:skmeans](#ATC-skmeans) |          6| 0.953|           0.917|       0.957|** |2,3,4,5    |
|[MAD:mclust](#MAD-mclust)   |          5| 0.929|           0.919|       0.966|*  |2          |
|[CV:hclust](#CV-hclust)     |          4| 0.921|           0.931|       0.951|*  |2,3        |
|[SD:hclust](#SD-hclust)     |          5| 0.919|           0.931|       0.952|*  |2,3,4      |
|[MAD:hclust](#MAD-hclust)   |          5| 0.917|           0.930|       0.956|*  |2,4        |
|[ATC:NMF](#ATC-NMF)         |          3| 0.917|           0.883|       0.951|*  |2          |
|[SD:pam](#SD-pam)           |          6| 0.908|           0.889|       0.913|*  |2,3,4,5    |
|[MAD:pam](#MAD-pam)         |          5| 0.905|           0.837|       0.896|*  |2,3,4      |
|[ATC:hclust](#ATC-hclust)   |          5| 0.903|           0.932|       0.963|*  |2,3        |

\*\*: 1-PAC > 0.95, \*: 1-PAC > 0.9




### CDF of consensus matrices

Cumulative distribution function curves of consensus matrix for all methods.




```r
collect_plots(res_list, fun = plot_ecdf)
```

![plot of chunk collect-plots](figure_cola/collect-plots-1.png)



### Consensus heatmap

Consensus heatmaps for all methods. ([What is a consensus heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_9))


<style type='text/css'>



.ui-helper-hidden {
	display: none;
}
.ui-helper-hidden-accessible {
	border: 0;
	clip: rect(0 0 0 0);
	height: 1px;
	margin: -1px;
	overflow: hidden;
	padding: 0;
	position: absolute;
	width: 1px;
}
.ui-helper-reset {
	margin: 0;
	padding: 0;
	border: 0;
	outline: 0;
	line-height: 1.3;
	text-decoration: none;
	font-size: 100%;
	list-style: none;
}
.ui-helper-clearfix:before,
.ui-helper-clearfix:after {
	content: "";
	display: table;
	border-collapse: collapse;
}
.ui-helper-clearfix:after {
	clear: both;
}
.ui-helper-zfix {
	width: 100%;
	height: 100%;
	top: 0;
	left: 0;
	position: absolute;
	opacity: 0;
	filter:Alpha(Opacity=0); 
}

.ui-front {
	z-index: 100;
}



.ui-state-disabled {
	cursor: default !important;
	pointer-events: none;
}



.ui-icon {
	display: inline-block;
	vertical-align: middle;
	margin-top: -.25em;
	position: relative;
	text-indent: -99999px;
	overflow: hidden;
	background-repeat: no-repeat;
}

.ui-widget-icon-block {
	left: 50%;
	margin-left: -8px;
	display: block;
}




.ui-widget-overlay {
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
}
.ui-accordion .ui-accordion-header {
	display: block;
	cursor: pointer;
	position: relative;
	margin: 2px 0 0 0;
	padding: .5em .5em .5em .7em;
	font-size: 100%;
}
.ui-accordion .ui-accordion-content {
	padding: 1em 2.2em;
	border-top: 0;
	overflow: auto;
}
.ui-autocomplete {
	position: absolute;
	top: 0;
	left: 0;
	cursor: default;
}
.ui-menu {
	list-style: none;
	padding: 0;
	margin: 0;
	display: block;
	outline: 0;
}
.ui-menu .ui-menu {
	position: absolute;
}
.ui-menu .ui-menu-item {
	margin: 0;
	cursor: pointer;
	
	list-style-image: url("data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7");
}
.ui-menu .ui-menu-item-wrapper {
	position: relative;
	padding: 3px 1em 3px .4em;
}
.ui-menu .ui-menu-divider {
	margin: 5px 0;
	height: 0;
	font-size: 0;
	line-height: 0;
	border-width: 1px 0 0 0;
}
.ui-menu .ui-state-focus,
.ui-menu .ui-state-active {
	margin: -1px;
}


.ui-menu-icons {
	position: relative;
}
.ui-menu-icons .ui-menu-item-wrapper {
	padding-left: 2em;
}


.ui-menu .ui-icon {
	position: absolute;
	top: 0;
	bottom: 0;
	left: .2em;
	margin: auto 0;
}


.ui-menu .ui-menu-icon {
	left: auto;
	right: 0;
}
.ui-button {
	padding: .4em 1em;
	display: inline-block;
	position: relative;
	line-height: normal;
	margin-right: .1em;
	cursor: pointer;
	vertical-align: middle;
	text-align: center;
	-webkit-user-select: none;
	-moz-user-select: none;
	-ms-user-select: none;
	user-select: none;

	
	overflow: visible;
}

.ui-button,
.ui-button:link,
.ui-button:visited,
.ui-button:hover,
.ui-button:active {
	text-decoration: none;
}


.ui-button-icon-only {
	width: 2em;
	box-sizing: border-box;
	text-indent: -9999px;
	white-space: nowrap;
}


input.ui-button.ui-button-icon-only {
	text-indent: 0;
}


.ui-button-icon-only .ui-icon {
	position: absolute;
	top: 50%;
	left: 50%;
	margin-top: -8px;
	margin-left: -8px;
}

.ui-button.ui-icon-notext .ui-icon {
	padding: 0;
	width: 2.1em;
	height: 2.1em;
	text-indent: -9999px;
	white-space: nowrap;

}

input.ui-button.ui-icon-notext .ui-icon {
	width: auto;
	height: auto;
	text-indent: 0;
	white-space: normal;
	padding: .4em 1em;
}



input.ui-button::-moz-focus-inner,
button.ui-button::-moz-focus-inner {
	border: 0;
	padding: 0;
}
.ui-controlgroup {
	vertical-align: middle;
	display: inline-block;
}
.ui-controlgroup > .ui-controlgroup-item {
	float: left;
	margin-left: 0;
	margin-right: 0;
}
.ui-controlgroup > .ui-controlgroup-item:focus,
.ui-controlgroup > .ui-controlgroup-item.ui-visual-focus {
	z-index: 9999;
}
.ui-controlgroup-vertical > .ui-controlgroup-item {
	display: block;
	float: none;
	width: 100%;
	margin-top: 0;
	margin-bottom: 0;
	text-align: left;
}
.ui-controlgroup-vertical .ui-controlgroup-item {
	box-sizing: border-box;
}
.ui-controlgroup .ui-controlgroup-label {
	padding: .4em 1em;
}
.ui-controlgroup .ui-controlgroup-label span {
	font-size: 80%;
}
.ui-controlgroup-horizontal .ui-controlgroup-label + .ui-controlgroup-item {
	border-left: none;
}
.ui-controlgroup-vertical .ui-controlgroup-label + .ui-controlgroup-item {
	border-top: none;
}
.ui-controlgroup-horizontal .ui-controlgroup-label.ui-widget-content {
	border-right: none;
}
.ui-controlgroup-vertical .ui-controlgroup-label.ui-widget-content {
	border-bottom: none;
}


.ui-controlgroup-vertical .ui-spinner-input {

	
	width: 75%;
	width: calc( 100% - 2.4em );
}
.ui-controlgroup-vertical .ui-spinner .ui-spinner-up {
	border-top-style: solid;
}

.ui-checkboxradio-label .ui-icon-background {
	box-shadow: inset 1px 1px 1px #ccc;
	border-radius: .12em;
	border: none;
}
.ui-checkboxradio-radio-label .ui-icon-background {
	width: 16px;
	height: 16px;
	border-radius: 1em;
	overflow: visible;
	border: none;
}
.ui-checkboxradio-radio-label.ui-checkboxradio-checked .ui-icon,
.ui-checkboxradio-radio-label.ui-checkboxradio-checked:hover .ui-icon {
	background-image: none;
	width: 8px;
	height: 8px;
	border-width: 4px;
	border-style: solid;
}
.ui-checkboxradio-disabled {
	pointer-events: none;
}
.ui-datepicker {
	width: 17em;
	padding: .2em .2em 0;
	display: none;
}
.ui-datepicker .ui-datepicker-header {
	position: relative;
	padding: .2em 0;
}
.ui-datepicker .ui-datepicker-prev,
.ui-datepicker .ui-datepicker-next {
	position: absolute;
	top: 2px;
	width: 1.8em;
	height: 1.8em;
}
.ui-datepicker .ui-datepicker-prev-hover,
.ui-datepicker .ui-datepicker-next-hover {
	top: 1px;
}
.ui-datepicker .ui-datepicker-prev {
	left: 2px;
}
.ui-datepicker .ui-datepicker-next {
	right: 2px;
}
.ui-datepicker .ui-datepicker-prev-hover {
	left: 1px;
}
.ui-datepicker .ui-datepicker-next-hover {
	right: 1px;
}
.ui-datepicker .ui-datepicker-prev span,
.ui-datepicker .ui-datepicker-next span {
	display: block;
	position: absolute;
	left: 50%;
	margin-left: -8px;
	top: 50%;
	margin-top: -8px;
}
.ui-datepicker .ui-datepicker-title {
	margin: 0 2.3em;
	line-height: 1.8em;
	text-align: center;
}
.ui-datepicker .ui-datepicker-title select {
	font-size: 1em;
	margin: 1px 0;
}
.ui-datepicker select.ui-datepicker-month,
.ui-datepicker select.ui-datepicker-year {
	width: 45%;
}
.ui-datepicker table {
	width: 100%;
	font-size: .9em;
	border-collapse: collapse;
	margin: 0 0 .4em;
}
.ui-datepicker th {
	padding: .7em .3em;
	text-align: center;
	font-weight: bold;
	border: 0;
}
.ui-datepicker td {
	border: 0;
	padding: 1px;
}
.ui-datepicker td span,
.ui-datepicker td a {
	display: block;
	padding: .2em;
	text-align: right;
	text-decoration: none;
}
.ui-datepicker .ui-datepicker-buttonpane {
	background-image: none;
	margin: .7em 0 0 0;
	padding: 0 .2em;
	border-left: 0;
	border-right: 0;
	border-bottom: 0;
}
.ui-datepicker .ui-datepicker-buttonpane button {
	float: right;
	margin: .5em .2em .4em;
	cursor: pointer;
	padding: .2em .6em .3em .6em;
	width: auto;
	overflow: visible;
}
.ui-datepicker .ui-datepicker-buttonpane button.ui-datepicker-current {
	float: left;
}


.ui-datepicker.ui-datepicker-multi {
	width: auto;
}
.ui-datepicker-multi .ui-datepicker-group {
	float: left;
}
.ui-datepicker-multi .ui-datepicker-group table {
	width: 95%;
	margin: 0 auto .4em;
}
.ui-datepicker-multi-2 .ui-datepicker-group {
	width: 50%;
}
.ui-datepicker-multi-3 .ui-datepicker-group {
	width: 33.3%;
}
.ui-datepicker-multi-4 .ui-datepicker-group {
	width: 25%;
}
.ui-datepicker-multi .ui-datepicker-group-last .ui-datepicker-header,
.ui-datepicker-multi .ui-datepicker-group-middle .ui-datepicker-header {
	border-left-width: 0;
}
.ui-datepicker-multi .ui-datepicker-buttonpane {
	clear: left;
}
.ui-datepicker-row-break {
	clear: both;
	width: 100%;
	font-size: 0;
}


.ui-datepicker-rtl {
	direction: rtl;
}
.ui-datepicker-rtl .ui-datepicker-prev {
	right: 2px;
	left: auto;
}
.ui-datepicker-rtl .ui-datepicker-next {
	left: 2px;
	right: auto;
}
.ui-datepicker-rtl .ui-datepicker-prev:hover {
	right: 1px;
	left: auto;
}
.ui-datepicker-rtl .ui-datepicker-next:hover {
	left: 1px;
	right: auto;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane {
	clear: right;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane button {
	float: left;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane button.ui-datepicker-current,
.ui-datepicker-rtl .ui-datepicker-group {
	float: right;
}
.ui-datepicker-rtl .ui-datepicker-group-last .ui-datepicker-header,
.ui-datepicker-rtl .ui-datepicker-group-middle .ui-datepicker-header {
	border-right-width: 0;
	border-left-width: 1px;
}


.ui-datepicker .ui-icon {
	display: block;
	text-indent: -99999px;
	overflow: hidden;
	background-repeat: no-repeat;
	left: .5em;
	top: .3em;
}
.ui-dialog {
	position: absolute;
	top: 0;
	left: 0;
	padding: .2em;
	outline: 0;
}
.ui-dialog .ui-dialog-titlebar {
	padding: .4em 1em;
	position: relative;
}
.ui-dialog .ui-dialog-title {
	float: left;
	margin: .1em 0;
	white-space: nowrap;
	width: 90%;
	overflow: hidden;
	text-overflow: ellipsis;
}
.ui-dialog .ui-dialog-titlebar-close {
	position: absolute;
	right: .3em;
	top: 50%;
	width: 20px;
	margin: -10px 0 0 0;
	padding: 1px;
	height: 20px;
}
.ui-dialog .ui-dialog-content {
	position: relative;
	border: 0;
	padding: .5em 1em;
	background: none;
	overflow: auto;
}
.ui-dialog .ui-dialog-buttonpane {
	text-align: left;
	border-width: 1px 0 0 0;
	background-image: none;
	margin-top: .5em;
	padding: .3em 1em .5em .4em;
}
.ui-dialog .ui-dialog-buttonpane .ui-dialog-buttonset {
	float: right;
}
.ui-dialog .ui-dialog-buttonpane button {
	margin: .5em .4em .5em 0;
	cursor: pointer;
}
.ui-dialog .ui-resizable-n {
	height: 2px;
	top: 0;
}
.ui-dialog .ui-resizable-e {
	width: 2px;
	right: 0;
}
.ui-dialog .ui-resizable-s {
	height: 2px;
	bottom: 0;
}
.ui-dialog .ui-resizable-w {
	width: 2px;
	left: 0;
}
.ui-dialog .ui-resizable-se,
.ui-dialog .ui-resizable-sw,
.ui-dialog .ui-resizable-ne,
.ui-dialog .ui-resizable-nw {
	width: 7px;
	height: 7px;
}
.ui-dialog .ui-resizable-se {
	right: 0;
	bottom: 0;
}
.ui-dialog .ui-resizable-sw {
	left: 0;
	bottom: 0;
}
.ui-dialog .ui-resizable-ne {
	right: 0;
	top: 0;
}
.ui-dialog .ui-resizable-nw {
	left: 0;
	top: 0;
}
.ui-draggable .ui-dialog-titlebar {
	cursor: move;
}
.ui-draggable-handle {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-resizable {
	position: relative;
}
.ui-resizable-handle {
	position: absolute;
	font-size: 0.1px;
	display: block;
	-ms-touch-action: none;
	touch-action: none;
}
.ui-resizable-disabled .ui-resizable-handle,
.ui-resizable-autohide .ui-resizable-handle {
	display: none;
}
.ui-resizable-n {
	cursor: n-resize;
	height: 7px;
	width: 100%;
	top: -5px;
	left: 0;
}
.ui-resizable-s {
	cursor: s-resize;
	height: 7px;
	width: 100%;
	bottom: -5px;
	left: 0;
}
.ui-resizable-e {
	cursor: e-resize;
	width: 7px;
	right: -5px;
	top: 0;
	height: 100%;
}
.ui-resizable-w {
	cursor: w-resize;
	width: 7px;
	left: -5px;
	top: 0;
	height: 100%;
}
.ui-resizable-se {
	cursor: se-resize;
	width: 12px;
	height: 12px;
	right: 1px;
	bottom: 1px;
}
.ui-resizable-sw {
	cursor: sw-resize;
	width: 9px;
	height: 9px;
	left: -5px;
	bottom: -5px;
}
.ui-resizable-nw {
	cursor: nw-resize;
	width: 9px;
	height: 9px;
	left: -5px;
	top: -5px;
}
.ui-resizable-ne {
	cursor: ne-resize;
	width: 9px;
	height: 9px;
	right: -5px;
	top: -5px;
}
.ui-progressbar {
	height: 2em;
	text-align: left;
	overflow: hidden;
}
.ui-progressbar .ui-progressbar-value {
	margin: -1px;
	height: 100%;
}
.ui-progressbar .ui-progressbar-overlay {
	background: url("data:image/gif;base64,R0lGODlhKAAoAIABAAAAAP///yH/C05FVFNDQVBFMi4wAwEAAAAh+QQJAQABACwAAAAAKAAoAAACkYwNqXrdC52DS06a7MFZI+4FHBCKoDeWKXqymPqGqxvJrXZbMx7Ttc+w9XgU2FB3lOyQRWET2IFGiU9m1frDVpxZZc6bfHwv4c1YXP6k1Vdy292Fb6UkuvFtXpvWSzA+HycXJHUXiGYIiMg2R6W459gnWGfHNdjIqDWVqemH2ekpObkpOlppWUqZiqr6edqqWQAAIfkECQEAAQAsAAAAACgAKAAAApSMgZnGfaqcg1E2uuzDmmHUBR8Qil95hiPKqWn3aqtLsS18y7G1SzNeowWBENtQd+T1JktP05nzPTdJZlR6vUxNWWjV+vUWhWNkWFwxl9VpZRedYcflIOLafaa28XdsH/ynlcc1uPVDZxQIR0K25+cICCmoqCe5mGhZOfeYSUh5yJcJyrkZWWpaR8doJ2o4NYq62lAAACH5BAkBAAEALAAAAAAoACgAAAKVDI4Yy22ZnINRNqosw0Bv7i1gyHUkFj7oSaWlu3ovC8GxNso5fluz3qLVhBVeT/Lz7ZTHyxL5dDalQWPVOsQWtRnuwXaFTj9jVVh8pma9JjZ4zYSj5ZOyma7uuolffh+IR5aW97cHuBUXKGKXlKjn+DiHWMcYJah4N0lYCMlJOXipGRr5qdgoSTrqWSq6WFl2ypoaUAAAIfkECQEAAQAsAAAAACgAKAAAApaEb6HLgd/iO7FNWtcFWe+ufODGjRfoiJ2akShbueb0wtI50zm02pbvwfWEMWBQ1zKGlLIhskiEPm9R6vRXxV4ZzWT2yHOGpWMyorblKlNp8HmHEb/lCXjcW7bmtXP8Xt229OVWR1fod2eWqNfHuMjXCPkIGNileOiImVmCOEmoSfn3yXlJWmoHGhqp6ilYuWYpmTqKUgAAIfkECQEAAQAsAAAAACgAKAAAApiEH6kb58biQ3FNWtMFWW3eNVcojuFGfqnZqSebuS06w5V80/X02pKe8zFwP6EFWOT1lDFk8rGERh1TTNOocQ61Hm4Xm2VexUHpzjymViHrFbiELsefVrn6XKfnt2Q9G/+Xdie499XHd2g4h7ioOGhXGJboGAnXSBnoBwKYyfioubZJ2Hn0RuRZaflZOil56Zp6iioKSXpUAAAh+QQJAQABACwAAAAAKAAoAAACkoQRqRvnxuI7kU1a1UU5bd5tnSeOZXhmn5lWK3qNTWvRdQxP8qvaC+/yaYQzXO7BMvaUEmJRd3TsiMAgswmNYrSgZdYrTX6tSHGZO73ezuAw2uxuQ+BbeZfMxsexY35+/Qe4J1inV0g4x3WHuMhIl2jXOKT2Q+VU5fgoSUI52VfZyfkJGkha6jmY+aaYdirq+lQAACH5BAkBAAEALAAAAAAoACgAAAKWBIKpYe0L3YNKToqswUlvznigd4wiR4KhZrKt9Upqip61i9E3vMvxRdHlbEFiEXfk9YARYxOZZD6VQ2pUunBmtRXo1Lf8hMVVcNl8JafV38aM2/Fu5V16Bn63r6xt97j09+MXSFi4BniGFae3hzbH9+hYBzkpuUh5aZmHuanZOZgIuvbGiNeomCnaxxap2upaCZsq+1kAACH5BAkBAAEALAAAAAAoACgAAAKXjI8By5zf4kOxTVrXNVlv1X0d8IGZGKLnNpYtm8Lr9cqVeuOSvfOW79D9aDHizNhDJidFZhNydEahOaDH6nomtJjp1tutKoNWkvA6JqfRVLHU/QUfau9l2x7G54d1fl995xcIGAdXqMfBNadoYrhH+Mg2KBlpVpbluCiXmMnZ2Sh4GBqJ+ckIOqqJ6LmKSllZmsoq6wpQAAAh+QQJAQABACwAAAAAKAAoAAAClYx/oLvoxuJDkU1a1YUZbJ59nSd2ZXhWqbRa2/gF8Gu2DY3iqs7yrq+xBYEkYvFSM8aSSObE+ZgRl1BHFZNr7pRCavZ5BW2142hY3AN/zWtsmf12p9XxxFl2lpLn1rseztfXZjdIWIf2s5dItwjYKBgo9yg5pHgzJXTEeGlZuenpyPmpGQoKOWkYmSpaSnqKileI2FAAACH5BAkBAAEALAAAAAAoACgAAAKVjB+gu+jG4kORTVrVhRlsnn2dJ3ZleFaptFrb+CXmO9OozeL5VfP99HvAWhpiUdcwkpBH3825AwYdU8xTqlLGhtCosArKMpvfa1mMRae9VvWZfeB2XfPkeLmm18lUcBj+p5dnN8jXZ3YIGEhYuOUn45aoCDkp16hl5IjYJvjWKcnoGQpqyPlpOhr3aElaqrq56Bq7VAAAOw==");
	height: 100%;
	filter: alpha(opacity=25); 
	opacity: 0.25;
}
.ui-progressbar-indeterminate .ui-progressbar-value {
	background-image: none;
}
.ui-selectable {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-selectable-helper {
	position: absolute;
	z-index: 100;
	border: 1px dotted black;
}
.ui-selectmenu-menu {
	padding: 0;
	margin: 0;
	position: absolute;
	top: 0;
	left: 0;
	display: none;
}
.ui-selectmenu-menu .ui-menu {
	overflow: auto;
	overflow-x: hidden;
	padding-bottom: 1px;
}
.ui-selectmenu-menu .ui-menu .ui-selectmenu-optgroup {
	font-size: 1em;
	font-weight: bold;
	line-height: 1.5;
	padding: 2px 0.4em;
	margin: 0.5em 0 0 0;
	height: auto;
	border: 0;
}
.ui-selectmenu-open {
	display: block;
}
.ui-selectmenu-text {
	display: block;
	margin-right: 20px;
	overflow: hidden;
	text-overflow: ellipsis;
}
.ui-selectmenu-button.ui-button {
	text-align: left;
	white-space: nowrap;
	width: 14em;
}
.ui-selectmenu-icon.ui-icon {
	float: right;
	margin-top: 0;
}
.ui-slider {
	position: relative;
	text-align: left;
}
.ui-slider .ui-slider-handle {
	position: absolute;
	z-index: 2;
	width: 1.2em;
	height: 1.2em;
	cursor: default;
	-ms-touch-action: none;
	touch-action: none;
}
.ui-slider .ui-slider-range {
	position: absolute;
	z-index: 1;
	font-size: .7em;
	display: block;
	border: 0;
	background-position: 0 0;
}


.ui-slider.ui-state-disabled .ui-slider-handle,
.ui-slider.ui-state-disabled .ui-slider-range {
	filter: inherit;
}

.ui-slider-horizontal {
	height: .8em;
}
.ui-slider-horizontal .ui-slider-handle {
	top: -.3em;
	margin-left: -.6em;
}
.ui-slider-horizontal .ui-slider-range {
	top: 0;
	height: 100%;
}
.ui-slider-horizontal .ui-slider-range-min {
	left: 0;
}
.ui-slider-horizontal .ui-slider-range-max {
	right: 0;
}

.ui-slider-vertical {
	width: .8em;
	height: 100px;
}
.ui-slider-vertical .ui-slider-handle {
	left: -.3em;
	margin-left: 0;
	margin-bottom: -.6em;
}
.ui-slider-vertical .ui-slider-range {
	left: 0;
	width: 100%;
}
.ui-slider-vertical .ui-slider-range-min {
	bottom: 0;
}
.ui-slider-vertical .ui-slider-range-max {
	top: 0;
}
.ui-sortable-handle {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-spinner {
	position: relative;
	display: inline-block;
	overflow: hidden;
	padding: 0;
	vertical-align: middle;
}
.ui-spinner-input {
	border: none;
	background: none;
	color: inherit;
	padding: .222em 0;
	margin: .2em 0;
	vertical-align: middle;
	margin-left: .4em;
	margin-right: 2em;
}
.ui-spinner-button {
	width: 1.6em;
	height: 50%;
	font-size: .5em;
	padding: 0;
	margin: 0;
	text-align: center;
	position: absolute;
	cursor: default;
	display: block;
	overflow: hidden;
	right: 0;
}

.ui-spinner a.ui-spinner-button {
	border-top-style: none;
	border-bottom-style: none;
	border-right-style: none;
}
.ui-spinner-up {
	top: 0;
}
.ui-spinner-down {
	bottom: 0;
}
.ui-tabs {
	position: relative;
	padding: .2em;
}
.ui-tabs .ui-tabs-nav {
	margin: 0;
	padding: .2em .2em 0;
}
.ui-tabs .ui-tabs-nav li {
	list-style: none;
	float: left;
	position: relative;
	top: 0;
	margin: 1px .2em 0 0;
	border-bottom-width: 0;
	padding: 0;
	white-space: nowrap;
}
.ui-tabs .ui-tabs-nav .ui-tabs-anchor {
	float: left;
	padding: .5em 1em;
	text-decoration: none;
}
.ui-tabs .ui-tabs-nav li.ui-tabs-active {
	margin-bottom: -1px;
	padding-bottom: 1px;
}
.ui-tabs .ui-tabs-nav li.ui-tabs-active .ui-tabs-anchor,
.ui-tabs .ui-tabs-nav li.ui-state-disabled .ui-tabs-anchor,
.ui-tabs .ui-tabs-nav li.ui-tabs-loading .ui-tabs-anchor {
	cursor: text;
}
.ui-tabs-collapsible .ui-tabs-nav li.ui-tabs-active .ui-tabs-anchor {
	cursor: pointer;
}
.ui-tabs .ui-tabs-panel {
	display: block;
	border-width: 0;
	padding: 1em 1.4em;
	background: none;
}
.ui-tooltip {
	padding: 8px;
	position: absolute;
	z-index: 9999;
	max-width: 300px;
}
body .ui-tooltip {
	border-width: 2px;
}

.ui-widget {
	font-family: Arial,Helvetica,sans-serif;
	font-size: 1em;
}
.ui-widget .ui-widget {
	font-size: 1em;
}
.ui-widget input,
.ui-widget select,
.ui-widget textarea,
.ui-widget button {
	font-family: Arial,Helvetica,sans-serif;
	font-size: 1em;
}
.ui-widget.ui-widget-content {
	border: 1px solid #c5c5c5;
}
.ui-widget-content {
	border: 1px solid #dddddd;
	background: #ffffff;
	color: #333333;
}
.ui-widget-content a {
	color: #333333;
}
.ui-widget-header {
	border: 1px solid #dddddd;
	background: #e9e9e9;
	color: #333333;
	font-weight: bold;
}
.ui-widget-header a {
	color: #333333;
}


.ui-state-default,
.ui-widget-content .ui-state-default,
.ui-widget-header .ui-state-default,
.ui-button,


html .ui-button.ui-state-disabled:hover,
html .ui-button.ui-state-disabled:active {
	border: 1px solid #c5c5c5;
	background: #f6f6f6;
	font-weight: normal;
	color: #454545;
}
.ui-state-default a,
.ui-state-default a:link,
.ui-state-default a:visited,
a.ui-button,
a:link.ui-button,
a:visited.ui-button,
.ui-button {
	color: #454545;
	text-decoration: none;
}
.ui-state-hover,
.ui-widget-content .ui-state-hover,
.ui-widget-header .ui-state-hover,
.ui-state-focus,
.ui-widget-content .ui-state-focus,
.ui-widget-header .ui-state-focus,
.ui-button:hover,
.ui-button:focus {
	border: 1px solid #cccccc;
	background: #ededed;
	font-weight: normal;
	color: #2b2b2b;
}
.ui-state-hover a,
.ui-state-hover a:hover,
.ui-state-hover a:link,
.ui-state-hover a:visited,
.ui-state-focus a,
.ui-state-focus a:hover,
.ui-state-focus a:link,
.ui-state-focus a:visited,
a.ui-button:hover,
a.ui-button:focus {
	color: #2b2b2b;
	text-decoration: none;
}

.ui-visual-focus {
	box-shadow: 0 0 3px 1px rgb(94, 158, 214);
}
.ui-state-active,
.ui-widget-content .ui-state-active,
.ui-widget-header .ui-state-active,
a.ui-button:active,
.ui-button:active,
.ui-button.ui-state-active:hover {
	border: 1px solid #003eff;
	background: #007fff;
	font-weight: normal;
	color: #ffffff;
}
.ui-icon-background,
.ui-state-active .ui-icon-background {
	border: #003eff;
	background-color: #ffffff;
}
.ui-state-active a,
.ui-state-active a:link,
.ui-state-active a:visited {
	color: #ffffff;
	text-decoration: none;
}


.ui-state-highlight,
.ui-widget-content .ui-state-highlight,
.ui-widget-header .ui-state-highlight {
	border: 1px solid #dad55e;
	background: #fffa90;
	color: #777620;
}
.ui-state-checked {
	border: 1px solid #dad55e;
	background: #fffa90;
}
.ui-state-highlight a,
.ui-widget-content .ui-state-highlight a,
.ui-widget-header .ui-state-highlight a {
	color: #777620;
}
.ui-state-error,
.ui-widget-content .ui-state-error,
.ui-widget-header .ui-state-error {
	border: 1px solid #f1a899;
	background: #fddfdf;
	color: #5f3f3f;
}
.ui-state-error a,
.ui-widget-content .ui-state-error a,
.ui-widget-header .ui-state-error a {
	color: #5f3f3f;
}
.ui-state-error-text,
.ui-widget-content .ui-state-error-text,
.ui-widget-header .ui-state-error-text {
	color: #5f3f3f;
}
.ui-priority-primary,
.ui-widget-content .ui-priority-primary,
.ui-widget-header .ui-priority-primary {
	font-weight: bold;
}
.ui-priority-secondary,
.ui-widget-content .ui-priority-secondary,
.ui-widget-header .ui-priority-secondary {
	opacity: .7;
	filter:Alpha(Opacity=70); 
	font-weight: normal;
}
.ui-state-disabled,
.ui-widget-content .ui-state-disabled,
.ui-widget-header .ui-state-disabled {
	opacity: .35;
	filter:Alpha(Opacity=35); 
	background-image: none;
}
.ui-state-disabled .ui-icon {
	filter:Alpha(Opacity=35); 
}




.ui-icon {
	width: 16px;
	height: 16px;
}
.ui-icon,
.ui-widget-content .ui-icon {
	background-image: url("images/ui-icons_444444_256x240.png");
}
.ui-widget-header .ui-icon {
	background-image: url("images/ui-icons_444444_256x240.png");
}
.ui-state-hover .ui-icon,
.ui-state-focus .ui-icon,
.ui-button:hover .ui-icon,
.ui-button:focus .ui-icon {
	background-image: url("images/ui-icons_555555_256x240.png");
}
.ui-state-active .ui-icon,
.ui-button:active .ui-icon {
	background-image: url("images/ui-icons_ffffff_256x240.png");
}
.ui-state-highlight .ui-icon,
.ui-button .ui-state-highlight.ui-icon {
	background-image: url("images/ui-icons_777620_256x240.png");
}
.ui-state-error .ui-icon,
.ui-state-error-text .ui-icon {
	background-image: url("images/ui-icons_cc0000_256x240.png");
}
.ui-button .ui-icon {
	background-image: url("images/ui-icons_777777_256x240.png");
}


.ui-icon-blank { background-position: 16px 16px; }
.ui-icon-caret-1-n { background-position: 0 0; }
.ui-icon-caret-1-ne { background-position: -16px 0; }
.ui-icon-caret-1-e { background-position: -32px 0; }
.ui-icon-caret-1-se { background-position: -48px 0; }
.ui-icon-caret-1-s { background-position: -65px 0; }
.ui-icon-caret-1-sw { background-position: -80px 0; }
.ui-icon-caret-1-w { background-position: -96px 0; }
.ui-icon-caret-1-nw { background-position: -112px 0; }
.ui-icon-caret-2-n-s { background-position: -128px 0; }
.ui-icon-caret-2-e-w { background-position: -144px 0; }
.ui-icon-triangle-1-n { background-position: 0 -16px; }
.ui-icon-triangle-1-ne { background-position: -16px -16px; }
.ui-icon-triangle-1-e { background-position: -32px -16px; }
.ui-icon-triangle-1-se { background-position: -48px -16px; }
.ui-icon-triangle-1-s { background-position: -65px -16px; }
.ui-icon-triangle-1-sw { background-position: -80px -16px; }
.ui-icon-triangle-1-w { background-position: -96px -16px; }
.ui-icon-triangle-1-nw { background-position: -112px -16px; }
.ui-icon-triangle-2-n-s { background-position: -128px -16px; }
.ui-icon-triangle-2-e-w { background-position: -144px -16px; }
.ui-icon-arrow-1-n { background-position: 0 -32px; }
.ui-icon-arrow-1-ne { background-position: -16px -32px; }
.ui-icon-arrow-1-e { background-position: -32px -32px; }
.ui-icon-arrow-1-se { background-position: -48px -32px; }
.ui-icon-arrow-1-s { background-position: -65px -32px; }
.ui-icon-arrow-1-sw { background-position: -80px -32px; }
.ui-icon-arrow-1-w { background-position: -96px -32px; }
.ui-icon-arrow-1-nw { background-position: -112px -32px; }
.ui-icon-arrow-2-n-s { background-position: -128px -32px; }
.ui-icon-arrow-2-ne-sw { background-position: -144px -32px; }
.ui-icon-arrow-2-e-w { background-position: -160px -32px; }
.ui-icon-arrow-2-se-nw { background-position: -176px -32px; }
.ui-icon-arrowstop-1-n { background-position: -192px -32px; }
.ui-icon-arrowstop-1-e { background-position: -208px -32px; }
.ui-icon-arrowstop-1-s { background-position: -224px -32px; }
.ui-icon-arrowstop-1-w { background-position: -240px -32px; }
.ui-icon-arrowthick-1-n { background-position: 1px -48px; }
.ui-icon-arrowthick-1-ne { background-position: -16px -48px; }
.ui-icon-arrowthick-1-e { background-position: -32px -48px; }
.ui-icon-arrowthick-1-se { background-position: -48px -48px; }
.ui-icon-arrowthick-1-s { background-position: -64px -48px; }
.ui-icon-arrowthick-1-sw { background-position: -80px -48px; }
.ui-icon-arrowthick-1-w { background-position: -96px -48px; }
.ui-icon-arrowthick-1-nw { background-position: -112px -48px; }
.ui-icon-arrowthick-2-n-s { background-position: -128px -48px; }
.ui-icon-arrowthick-2-ne-sw { background-position: -144px -48px; }
.ui-icon-arrowthick-2-e-w { background-position: -160px -48px; }
.ui-icon-arrowthick-2-se-nw { background-position: -176px -48px; }
.ui-icon-arrowthickstop-1-n { background-position: -192px -48px; }
.ui-icon-arrowthickstop-1-e { background-position: -208px -48px; }
.ui-icon-arrowthickstop-1-s { background-position: -224px -48px; }
.ui-icon-arrowthickstop-1-w { background-position: -240px -48px; }
.ui-icon-arrowreturnthick-1-w { background-position: 0 -64px; }
.ui-icon-arrowreturnthick-1-n { background-position: -16px -64px; }
.ui-icon-arrowreturnthick-1-e { background-position: -32px -64px; }
.ui-icon-arrowreturnthick-1-s { background-position: -48px -64px; }
.ui-icon-arrowreturn-1-w { background-position: -64px -64px; }
.ui-icon-arrowreturn-1-n { background-position: -80px -64px; }
.ui-icon-arrowreturn-1-e { background-position: -96px -64px; }
.ui-icon-arrowreturn-1-s { background-position: -112px -64px; }
.ui-icon-arrowrefresh-1-w { background-position: -128px -64px; }
.ui-icon-arrowrefresh-1-n { background-position: -144px -64px; }
.ui-icon-arrowrefresh-1-e { background-position: -160px -64px; }
.ui-icon-arrowrefresh-1-s { background-position: -176px -64px; }
.ui-icon-arrow-4 { background-position: 0 -80px; }
.ui-icon-arrow-4-diag { background-position: -16px -80px; }
.ui-icon-extlink { background-position: -32px -80px; }
.ui-icon-newwin { background-position: -48px -80px; }
.ui-icon-refresh { background-position: -64px -80px; }
.ui-icon-shuffle { background-position: -80px -80px; }
.ui-icon-transfer-e-w { background-position: -96px -80px; }
.ui-icon-transferthick-e-w { background-position: -112px -80px; }
.ui-icon-folder-collapsed { background-position: 0 -96px; }
.ui-icon-folder-open { background-position: -16px -96px; }
.ui-icon-document { background-position: -32px -96px; }
.ui-icon-document-b { background-position: -48px -96px; }
.ui-icon-note { background-position: -64px -96px; }
.ui-icon-mail-closed { background-position: -80px -96px; }
.ui-icon-mail-open { background-position: -96px -96px; }
.ui-icon-suitcase { background-position: -112px -96px; }
.ui-icon-comment { background-position: -128px -96px; }
.ui-icon-person { background-position: -144px -96px; }
.ui-icon-print { background-position: -160px -96px; }
.ui-icon-trash { background-position: -176px -96px; }
.ui-icon-locked { background-position: -192px -96px; }
.ui-icon-unlocked { background-position: -208px -96px; }
.ui-icon-bookmark { background-position: -224px -96px; }
.ui-icon-tag { background-position: -240px -96px; }
.ui-icon-home { background-position: 0 -112px; }
.ui-icon-flag { background-position: -16px -112px; }
.ui-icon-calendar { background-position: -32px -112px; }
.ui-icon-cart { background-position: -48px -112px; }
.ui-icon-pencil { background-position: -64px -112px; }
.ui-icon-clock { background-position: -80px -112px; }
.ui-icon-disk { background-position: -96px -112px; }
.ui-icon-calculator { background-position: -112px -112px; }
.ui-icon-zoomin { background-position: -128px -112px; }
.ui-icon-zoomout { background-position: -144px -112px; }
.ui-icon-search { background-position: -160px -112px; }
.ui-icon-wrench { background-position: -176px -112px; }
.ui-icon-gear { background-position: -192px -112px; }
.ui-icon-heart { background-position: -208px -112px; }
.ui-icon-star { background-position: -224px -112px; }
.ui-icon-link { background-position: -240px -112px; }
.ui-icon-cancel { background-position: 0 -128px; }
.ui-icon-plus { background-position: -16px -128px; }
.ui-icon-plusthick { background-position: -32px -128px; }
.ui-icon-minus { background-position: -48px -128px; }
.ui-icon-minusthick { background-position: -64px -128px; }
.ui-icon-close { background-position: -80px -128px; }
.ui-icon-closethick { background-position: -96px -128px; }
.ui-icon-key { background-position: -112px -128px; }
.ui-icon-lightbulb { background-position: -128px -128px; }
.ui-icon-scissors { background-position: -144px -128px; }
.ui-icon-clipboard { background-position: -160px -128px; }
.ui-icon-copy { background-position: -176px -128px; }
.ui-icon-contact { background-position: -192px -128px; }
.ui-icon-image { background-position: -208px -128px; }
.ui-icon-video { background-position: -224px -128px; }
.ui-icon-script { background-position: -240px -128px; }
.ui-icon-alert { background-position: 0 -144px; }
.ui-icon-info { background-position: -16px -144px; }
.ui-icon-notice { background-position: -32px -144px; }
.ui-icon-help { background-position: -48px -144px; }
.ui-icon-check { background-position: -64px -144px; }
.ui-icon-bullet { background-position: -80px -144px; }
.ui-icon-radio-on { background-position: -96px -144px; }
.ui-icon-radio-off { background-position: -112px -144px; }
.ui-icon-pin-w { background-position: -128px -144px; }
.ui-icon-pin-s { background-position: -144px -144px; }
.ui-icon-play { background-position: 0 -160px; }
.ui-icon-pause { background-position: -16px -160px; }
.ui-icon-seek-next { background-position: -32px -160px; }
.ui-icon-seek-prev { background-position: -48px -160px; }
.ui-icon-seek-end { background-position: -64px -160px; }
.ui-icon-seek-start { background-position: -80px -160px; }

.ui-icon-seek-first { background-position: -80px -160px; }
.ui-icon-stop { background-position: -96px -160px; }
.ui-icon-eject { background-position: -112px -160px; }
.ui-icon-volume-off { background-position: -128px -160px; }
.ui-icon-volume-on { background-position: -144px -160px; }
.ui-icon-power { background-position: 0 -176px; }
.ui-icon-signal-diag { background-position: -16px -176px; }
.ui-icon-signal { background-position: -32px -176px; }
.ui-icon-battery-0 { background-position: -48px -176px; }
.ui-icon-battery-1 { background-position: -64px -176px; }
.ui-icon-battery-2 { background-position: -80px -176px; }
.ui-icon-battery-3 { background-position: -96px -176px; }
.ui-icon-circle-plus { background-position: 0 -192px; }
.ui-icon-circle-minus { background-position: -16px -192px; }
.ui-icon-circle-close { background-position: -32px -192px; }
.ui-icon-circle-triangle-e { background-position: -48px -192px; }
.ui-icon-circle-triangle-s { background-position: -64px -192px; }
.ui-icon-circle-triangle-w { background-position: -80px -192px; }
.ui-icon-circle-triangle-n { background-position: -96px -192px; }
.ui-icon-circle-arrow-e { background-position: -112px -192px; }
.ui-icon-circle-arrow-s { background-position: -128px -192px; }
.ui-icon-circle-arrow-w { background-position: -144px -192px; }
.ui-icon-circle-arrow-n { background-position: -160px -192px; }
.ui-icon-circle-zoomin { background-position: -176px -192px; }
.ui-icon-circle-zoomout { background-position: -192px -192px; }
.ui-icon-circle-check { background-position: -208px -192px; }
.ui-icon-circlesmall-plus { background-position: 0 -208px; }
.ui-icon-circlesmall-minus { background-position: -16px -208px; }
.ui-icon-circlesmall-close { background-position: -32px -208px; }
.ui-icon-squaresmall-plus { background-position: -48px -208px; }
.ui-icon-squaresmall-minus { background-position: -64px -208px; }
.ui-icon-squaresmall-close { background-position: -80px -208px; }
.ui-icon-grip-dotted-vertical { background-position: 0 -224px; }
.ui-icon-grip-dotted-horizontal { background-position: -16px -224px; }
.ui-icon-grip-solid-vertical { background-position: -32px -224px; }
.ui-icon-grip-solid-horizontal { background-position: -48px -224px; }
.ui-icon-gripsmall-diagonal-se { background-position: -64px -224px; }
.ui-icon-grip-diagonal-se { background-position: -80px -224px; }





.ui-corner-all,
.ui-corner-top,
.ui-corner-left,
.ui-corner-tl {
	border-top-left-radius: 3px;
}
.ui-corner-all,
.ui-corner-top,
.ui-corner-right,
.ui-corner-tr {
	border-top-right-radius: 3px;
}
.ui-corner-all,
.ui-corner-bottom,
.ui-corner-left,
.ui-corner-bl {
	border-bottom-left-radius: 3px;
}
.ui-corner-all,
.ui-corner-bottom,
.ui-corner-right,
.ui-corner-br {
	border-bottom-right-radius: 3px;
}


.ui-widget-overlay {
	background: #aaaaaa;
	opacity: .3;
	filter: Alpha(Opacity=30); 
}
.ui-widget-shadow {
	-webkit-box-shadow: 0px 0px 5px #666666;
	box-shadow: 0px 0px 5px #666666;
} 
</style>
<script src='js/jquery-1.12.4.js'></script>
<script src='js/jquery-ui.js'></script>

<script>
$( function() {
	$( '#tabs-collect-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-collect-consensus-heatmap'>
<ul>
<li><a href='#tab-collect-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-collect-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-collect-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-collect-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-collect-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-collect-consensus-heatmap-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-1-1.png" alt="plot of chunk tab-collect-consensus-heatmap-1"/></p>

</div>
<div id='tab-collect-consensus-heatmap-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-2-1.png" alt="plot of chunk tab-collect-consensus-heatmap-2"/></p>

</div>
<div id='tab-collect-consensus-heatmap-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-3-1.png" alt="plot of chunk tab-collect-consensus-heatmap-3"/></p>

</div>
<div id='tab-collect-consensus-heatmap-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-4-1.png" alt="plot of chunk tab-collect-consensus-heatmap-4"/></p>

</div>
<div id='tab-collect-consensus-heatmap-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-5-1.png" alt="plot of chunk tab-collect-consensus-heatmap-5"/></p>

</div>
</div>



### Membership heatmap

Membership heatmaps for all methods. ([What is a membership heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_12))


<script>
$( function() {
	$( '#tabs-collect-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-collect-membership-heatmap'>
<ul>
<li><a href='#tab-collect-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-collect-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-collect-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-collect-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-collect-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-collect-membership-heatmap-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-1-1.png" alt="plot of chunk tab-collect-membership-heatmap-1"/></p>

</div>
<div id='tab-collect-membership-heatmap-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-2-1.png" alt="plot of chunk tab-collect-membership-heatmap-2"/></p>

</div>
<div id='tab-collect-membership-heatmap-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-3-1.png" alt="plot of chunk tab-collect-membership-heatmap-3"/></p>

</div>
<div id='tab-collect-membership-heatmap-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-4-1.png" alt="plot of chunk tab-collect-membership-heatmap-4"/></p>

</div>
<div id='tab-collect-membership-heatmap-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-5-1.png" alt="plot of chunk tab-collect-membership-heatmap-5"/></p>

</div>
</div>



### Signature heatmap

Signature heatmaps for all methods. ([What is a signature heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_22))


Note in following heatmaps, rows are scaled.



<script>
$( function() {
	$( '#tabs-collect-get-signatures' ).tabs();
} );
</script>
<div id='tabs-collect-get-signatures'>
<ul>
<li><a href='#tab-collect-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-collect-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-collect-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-collect-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-collect-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-collect-get-signatures-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-1-1.png" alt="plot of chunk tab-collect-get-signatures-1"/></p>

</div>
<div id='tab-collect-get-signatures-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-2-1.png" alt="plot of chunk tab-collect-get-signatures-2"/></p>

</div>
<div id='tab-collect-get-signatures-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-3-1.png" alt="plot of chunk tab-collect-get-signatures-3"/></p>

</div>
<div id='tab-collect-get-signatures-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-4-1.png" alt="plot of chunk tab-collect-get-signatures-4"/></p>

</div>
<div id='tab-collect-get-signatures-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-5-1.png" alt="plot of chunk tab-collect-get-signatures-5"/></p>

</div>
</div>



### Statistics table

The statistics used for measuring the stability of consensus partitioning.
([How are they
defined?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13))


<script>
$( function() {
	$( '#tabs-get-stats-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-get-stats-from-consensus-partition-list'>
<ul>
<li><a href='#tab-get-stats-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-get-stats-from-consensus-partition-list-1'>
<pre><code class="r">get_stats(res_list, k = 2)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      2     1           1.000       1.000          0.510 0.491   0.491
#&gt; CV:NMF      2     1           1.000       1.000          0.510 0.491   0.491
#&gt; MAD:NMF     2     1           1.000       1.000          0.510 0.491   0.491
#&gt; ATC:NMF     2     1           1.000       1.000          0.510 0.491   0.491
#&gt; SD:skmeans  2     1           1.000       1.000          0.510 0.491   0.491
#&gt; CV:skmeans  2     1           1.000       1.000          0.510 0.491   0.491
#&gt; MAD:skmeans 2     1           1.000       1.000          0.510 0.491   0.491
#&gt; ATC:skmeans 2     1           1.000       1.000          0.507 0.493   0.493
#&gt; SD:mclust   2     1           1.000       1.000          0.510 0.491   0.491
#&gt; CV:mclust   2     1           1.000       1.000          0.510 0.491   0.491
#&gt; MAD:mclust  2     1           1.000       1.000          0.510 0.491   0.491
#&gt; ATC:mclust  2     1           1.000       1.000          0.510 0.491   0.491
#&gt; SD:kmeans   2     1           1.000       1.000          0.510 0.491   0.491
#&gt; CV:kmeans   2     1           1.000       1.000          0.510 0.491   0.491
#&gt; MAD:kmeans  2     1           1.000       1.000          0.510 0.491   0.491
#&gt; ATC:kmeans  2     1           1.000       1.000          0.507 0.493   0.493
#&gt; SD:pam      2     1           1.000       1.000          0.510 0.491   0.491
#&gt; CV:pam      2     1           0.991       0.996          0.509 0.491   0.491
#&gt; MAD:pam     2     1           0.999       0.999          0.509 0.491   0.491
#&gt; ATC:pam     2     1           1.000       1.000          0.498 0.502   0.502
#&gt; SD:hclust   2     1           0.997       0.997          0.509 0.491   0.491
#&gt; CV:hclust   2     1           1.000       1.000          0.510 0.491   0.491
#&gt; MAD:hclust  2     1           1.000       1.000          0.510 0.491   0.491
#&gt; ATC:hclust  2     1           1.000       1.000          0.507 0.493   0.493
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-2'>
<pre><code class="r">get_stats(res_list, k = 3)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      3 0.842           0.819       0.914         0.1226 0.946   0.889
#&gt; CV:NMF      3 0.752           0.827       0.905         0.1335 0.965   0.929
#&gt; MAD:NMF     3 0.853           0.829       0.919         0.1490 0.906   0.811
#&gt; ATC:NMF     3 0.917           0.883       0.951         0.2624 0.864   0.724
#&gt; SD:skmeans  3 1.000           0.963       0.983         0.2771 0.835   0.670
#&gt; CV:skmeans  3 1.000           0.968       0.978         0.2687 0.864   0.724
#&gt; MAD:skmeans 3 1.000           0.968       0.982         0.2741 0.863   0.720
#&gt; ATC:skmeans 3 1.000           0.980       0.990         0.2886 0.853   0.702
#&gt; SD:mclust   3 1.000           0.974       0.979         0.0841 0.965   0.929
#&gt; CV:mclust   3 0.734           0.860       0.848         0.2110 0.882   0.760
#&gt; MAD:mclust  3 0.892           0.956       0.963         0.0955 0.965   0.929
#&gt; ATC:mclust  3 0.889           0.975       0.972         0.1909 0.897   0.791
#&gt; SD:kmeans   3 0.742           0.881       0.807         0.2476 0.864   0.724
#&gt; CV:kmeans   3 0.687           0.801       0.794         0.2335 1.000   1.000
#&gt; MAD:kmeans  3 0.746           0.857       0.801         0.2494 0.864   0.724
#&gt; ATC:kmeans  3 0.744           0.794       0.791         0.2559 0.798   0.607
#&gt; SD:pam      3 0.914           0.938       0.967         0.2701 0.841   0.681
#&gt; CV:pam      3 0.699           0.583       0.794         0.2356 0.905   0.806
#&gt; MAD:pam     3 0.946           0.949       0.975         0.2726 0.841   0.681
#&gt; ATC:pam     3 0.978           0.966       0.984         0.3277 0.837   0.676
#&gt; SD:hclust   3 0.963           0.947       0.958         0.1934 0.887   0.770
#&gt; CV:hclust   3 1.000           0.975       0.991         0.0840 0.950   0.899
#&gt; MAD:hclust  3 0.755           0.950       0.931         0.2104 0.887   0.770
#&gt; ATC:hclust  3 1.000           0.990       0.994         0.1964 0.898   0.794
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-3'>
<pre><code class="r">get_stats(res_list, k = 4)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      4 0.633           0.524       0.770         0.1448 0.907   0.792
#&gt; CV:NMF      4 0.707           0.553       0.815         0.1394 0.913   0.810
#&gt; MAD:NMF     4 0.649           0.653       0.792         0.1161 0.910   0.804
#&gt; ATC:NMF     4 0.715           0.723       0.875         0.1198 0.858   0.631
#&gt; SD:skmeans  4 1.000           0.975       0.990         0.1545 0.895   0.701
#&gt; CV:skmeans  4 0.868           0.848       0.906         0.1565 0.897   0.711
#&gt; MAD:skmeans 4 1.000           0.967       0.986         0.1627 0.891   0.693
#&gt; ATC:skmeans 4 0.946           0.868       0.955         0.1126 0.928   0.793
#&gt; SD:mclust   4 0.738           0.826       0.872         0.3024 0.777   0.520
#&gt; CV:mclust   4 0.631           0.418       0.714         0.0847 0.885   0.749
#&gt; MAD:mclust  4 0.887           0.878       0.929         0.3127 0.813   0.594
#&gt; ATC:mclust  4 0.885           0.871       0.937         0.1892 0.754   0.476
#&gt; SD:kmeans   4 0.680           0.911       0.861         0.1286 0.872   0.648
#&gt; CV:kmeans   4 0.651           0.604       0.754         0.1281 0.769   0.530
#&gt; MAD:kmeans  4 0.697           0.893       0.858         0.1288 0.872   0.648
#&gt; ATC:kmeans  4 0.700           0.915       0.848         0.1253 0.889   0.678
#&gt; SD:pam      4 0.911           0.936       0.965         0.1500 0.897   0.708
#&gt; CV:pam      4 0.704           0.741       0.887         0.2019 0.769   0.466
#&gt; MAD:pam     4 0.910           0.906       0.959         0.1588 0.889   0.687
#&gt; ATC:pam     4 1.000           0.979       0.991         0.1390 0.886   0.675
#&gt; SD:hclust   4 0.946           0.937       0.950         0.2201 0.863   0.637
#&gt; CV:hclust   4 0.921           0.931       0.951         0.1555 0.921   0.821
#&gt; MAD:hclust  4 0.907           0.946       0.959         0.2077 0.863   0.637
#&gt; ATC:hclust  4 0.773           0.680       0.845         0.1475 0.879   0.692
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-4'>
<pre><code class="r">get_stats(res_list, k = 5)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      5 0.645           0.748       0.803         0.1145 0.772   0.440
#&gt; CV:NMF      5 0.759           0.838       0.883         0.1429 0.778   0.454
#&gt; MAD:NMF     5 0.694           0.779       0.811         0.1239 0.759   0.460
#&gt; ATC:NMF     5 0.693           0.663       0.806         0.0571 0.922   0.731
#&gt; SD:skmeans  5 1.000           0.980       0.988         0.0323 0.971   0.884
#&gt; CV:skmeans  5 0.871           0.891       0.927         0.0384 0.971   0.884
#&gt; MAD:skmeans 5 1.000           0.966       0.982         0.0259 0.977   0.905
#&gt; ATC:skmeans 5 0.957           0.930       0.970         0.0308 0.967   0.881
#&gt; SD:mclust   5 0.958           0.883       0.945         0.0718 0.959   0.843
#&gt; CV:mclust   5 0.833           0.886       0.929         0.1498 0.765   0.470
#&gt; MAD:mclust  5 0.929           0.919       0.966         0.0423 0.919   0.726
#&gt; ATC:mclust  5 1.000           0.997       0.999         0.0741 0.921   0.739
#&gt; SD:kmeans   5 0.802           0.781       0.841         0.0682 0.994   0.975
#&gt; CV:kmeans   5 0.634           0.764       0.748         0.0662 0.876   0.583
#&gt; MAD:kmeans  5 0.630           0.743       0.828         0.0647 0.994   0.975
#&gt; ATC:kmeans  5 0.754           0.843       0.841         0.0692 0.949   0.796
#&gt; SD:pam      5 0.901           0.863       0.906         0.0556 0.947   0.801
#&gt; CV:pam      5 0.748           0.680       0.809         0.0451 0.919   0.690
#&gt; MAD:pam     5 0.905           0.837       0.896         0.0519 0.947   0.796
#&gt; ATC:pam     5 0.984           0.950       0.977         0.0555 0.928   0.727
#&gt; SD:hclust   5 0.919           0.931       0.952         0.0229 0.984   0.934
#&gt; CV:hclust   5 0.843           0.867       0.937         0.2040 0.863   0.621
#&gt; MAD:hclust  5 0.917           0.930       0.956         0.0204 0.984   0.934
#&gt; ATC:hclust  5 0.903           0.932       0.963         0.0927 0.879   0.612
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-5'>
<pre><code class="r">get_stats(res_list, k = 6)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      6 0.668           0.779       0.823         0.0464 0.952   0.804
#&gt; CV:NMF      6 0.820           0.806       0.889         0.0442 0.954   0.802
#&gt; MAD:NMF     6 0.655           0.734       0.812         0.0264 0.972   0.883
#&gt; ATC:NMF     6 0.671           0.534       0.758         0.0388 0.883   0.579
#&gt; SD:skmeans  6 0.904           0.857       0.919         0.0253 0.998   0.993
#&gt; CV:skmeans  6 0.879           0.874       0.910         0.0433 0.962   0.835
#&gt; MAD:skmeans 6 0.896           0.871       0.915         0.0264 0.989   0.953
#&gt; ATC:skmeans 6 0.953           0.917       0.957         0.0312 0.968   0.875
#&gt; SD:mclust   6 0.877           0.793       0.898         0.0383 0.922   0.687
#&gt; CV:mclust   6 0.854           0.779       0.886         0.0290 0.991   0.960
#&gt; MAD:mclust  6 0.897           0.915       0.922         0.0488 0.915   0.667
#&gt; ATC:mclust  6 1.000           0.971       0.989         0.0542 0.958   0.812
#&gt; SD:kmeans   6 0.832           0.662       0.786         0.0449 0.985   0.937
#&gt; CV:kmeans   6 0.719           0.787       0.783         0.0521 0.974   0.881
#&gt; MAD:kmeans  6 0.811           0.745       0.780         0.0494 0.964   0.849
#&gt; ATC:kmeans  6 0.848           0.776       0.836         0.0509 0.962   0.827
#&gt; SD:pam      6 0.908           0.889       0.913         0.0298 0.971   0.868
#&gt; CV:pam      6 0.816           0.762       0.815         0.0343 0.934   0.711
#&gt; MAD:pam     6 0.866           0.849       0.881         0.0306 0.977   0.892
#&gt; ATC:pam     6 0.984           0.938       0.973         0.0121 0.989   0.949
#&gt; SD:hclust   6 0.977           0.929       0.971         0.0240 0.998   0.993
#&gt; CV:hclust   6 0.784           0.722       0.845         0.0479 0.967   0.852
#&gt; MAD:hclust  6 0.979           0.918       0.973         0.0223 0.998   0.993
#&gt; ATC:hclust  6 0.892           0.864       0.933         0.0113 0.989   0.955
</code></pre>

</div>
</div>

Following heatmap plots the partition for each combination of methods and the
lightness correspond to the silhouette scores for samples in each method. On
top the consensus subgroup is inferred from all methods by taking the mean
silhouette scores as weight.


<script>
$( function() {
	$( '#tabs-collect-stats-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-collect-stats-from-consensus-partition-list'>
<ul>
<li><a href='#tab-collect-stats-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-collect-stats-from-consensus-partition-list-1'>
<pre><code class="r">collect_stats(res_list, k = 2)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-1-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-1"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-2'>
<pre><code class="r">collect_stats(res_list, k = 3)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-2-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-2"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-3'>
<pre><code class="r">collect_stats(res_list, k = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-3-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-3"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-4'>
<pre><code class="r">collect_stats(res_list, k = 5)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-4-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-4"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-5'>
<pre><code class="r">collect_stats(res_list, k = 6)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-5-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-5"/></p>

</div>
</div>

### Partition from all methods



Collect partitions from all methods:


<script>
$( function() {
	$( '#tabs-collect-classes-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-collect-classes-from-consensus-partition-list'>
<ul>
<li><a href='#tab-collect-classes-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-collect-classes-from-consensus-partition-list-1'>
<pre><code class="r">collect_classes(res_list, k = 2)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-1-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-1"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-2'>
<pre><code class="r">collect_classes(res_list, k = 3)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-2-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-2"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-3'>
<pre><code class="r">collect_classes(res_list, k = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-3-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-3"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-4'>
<pre><code class="r">collect_classes(res_list, k = 5)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-4-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-4"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-5'>
<pre><code class="r">collect_classes(res_list, k = 6)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-5-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-5"/></p>

</div>
</div>



### Top rows overlap


Overlap of top rows from different top-row methods:


<script>
$( function() {
	$( '#tabs-top-rows-overlap-by-euler' ).tabs();
} );
</script>
<div id='tabs-top-rows-overlap-by-euler'>
<ul>
<li><a href='#tab-top-rows-overlap-by-euler-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-overlap-by-euler-1'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 1000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-1-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-1"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-2'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 2000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-2-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-2"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-3'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 3000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-3-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-3"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-4'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 4000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-4-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-4"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-5'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 5000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-5-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-5"/></p>

</div>
</div>

Also visualize the correspondance of rankings between different top-row methods:


<script>
$( function() {
	$( '#tabs-top-rows-overlap-by-correspondance' ).tabs();
} );
</script>
<div id='tabs-top-rows-overlap-by-correspondance'>
<ul>
<li><a href='#tab-top-rows-overlap-by-correspondance-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-overlap-by-correspondance-1'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 1000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-1-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-1"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-2'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 2000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-2-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-2"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-3'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 3000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-3-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-3"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-4'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 4000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-4-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-4"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-5'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 5000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-5-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-5"/></p>

</div>
</div>


Heatmaps of the top rows:



<script>
$( function() {
	$( '#tabs-top-rows-heatmap' ).tabs();
} );
</script>
<div id='tabs-top-rows-heatmap'>
<ul>
<li><a href='#tab-top-rows-heatmap-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-heatmap-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-heatmap-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-heatmap-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-heatmap-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-heatmap-1'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 1000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-1-1.png" alt="plot of chunk tab-top-rows-heatmap-1"/></p>

</div>
<div id='tab-top-rows-heatmap-2'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 2000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-2-1.png" alt="plot of chunk tab-top-rows-heatmap-2"/></p>

</div>
<div id='tab-top-rows-heatmap-3'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 3000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-3-1.png" alt="plot of chunk tab-top-rows-heatmap-3"/></p>

</div>
<div id='tab-top-rows-heatmap-4'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 4000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-4-1.png" alt="plot of chunk tab-top-rows-heatmap-4"/></p>

</div>
<div id='tab-top-rows-heatmap-5'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 5000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-5-1.png" alt="plot of chunk tab-top-rows-heatmap-5"/></p>

</div>
</div>



 
## Results for each method


---------------------------------------------------




### SD:hclust*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "hclust"]
# you can also extract it by
# res = res_list["SD:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16868 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 5.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-hclust-collect-plots](figure_cola/SD-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-hclust-select-partition-number](figure_cola/SD-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.997       0.997         0.5092 0.491   0.491
#> 3 3 0.963           0.947       0.958         0.1934 0.887   0.770
#> 4 4 0.946           0.937       0.950         0.2201 0.863   0.637
#> 5 5 0.919           0.931       0.952         0.0229 0.984   0.934
#> 6 6 0.977           0.929       0.971         0.0240 0.998   0.993
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 5
#> attr(,"optional")
#> [1] 2 3 4
```

There is also optional best $k$ = 2 3 4 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-classes'>
<ul>
<li><a href='#tab-SD-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-hclust-get-classes-1'>
<p><a id='tab-SD-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1927048     1  0.0672      0.996 0.992 0.008
#&gt; SRR1927061     2  0.0000      0.998 0.000 1.000
#&gt; SRR1927060     1  0.0672      0.996 0.992 0.008
#&gt; SRR1927059     2  0.0000      0.998 0.000 1.000
#&gt; SRR1927058     1  0.0672      0.996 0.992 0.008
#&gt; SRR1927057     2  0.0000      0.998 0.000 1.000
#&gt; SRR1927055     2  0.0672      0.993 0.008 0.992
#&gt; SRR1927056     1  0.0000      0.996 1.000 0.000
#&gt; SRR1927054     1  0.0672      0.996 0.992 0.008
#&gt; SRR1927052     1  0.0000      0.996 1.000 0.000
#&gt; SRR1927053     2  0.0000      0.998 0.000 1.000
#&gt; SRR1927051     2  0.0000      0.998 0.000 1.000
#&gt; SRR1927050     1  0.0000      0.996 1.000 0.000
#&gt; SRR1927049     2  0.0000      0.998 0.000 1.000
#&gt; SRR1927047     2  0.0000      0.998 0.000 1.000
#&gt; SRR1927046     1  0.0672      0.996 0.992 0.008
#&gt; SRR1927045     2  0.0000      0.998 0.000 1.000
#&gt; SRR1927044     1  0.0672      0.996 0.992 0.008
#&gt; SRR1927043     2  0.0000      0.998 0.000 1.000
#&gt; SRR1927042     1  0.0672      0.996 0.992 0.008
#&gt; SRR1927040     1  0.0672      0.996 0.992 0.008
#&gt; SRR1927039     2  0.0000      0.998 0.000 1.000
#&gt; SRR1927038     1  0.0672      0.996 0.992 0.008
#&gt; SRR1927037     2  0.0000      0.998 0.000 1.000
#&gt; SRR1927036     1  0.0672      0.996 0.992 0.008
#&gt; SRR1927035     2  0.0000      0.998 0.000 1.000
#&gt; SRR1927034     1  0.0000      0.996 1.000 0.000
#&gt; SRR1927033     2  0.0672      0.993 0.008 0.992
#&gt; SRR1927032     1  0.0672      0.996 0.992 0.008
#&gt; SRR1927031     2  0.0000      0.998 0.000 1.000
#&gt; SRR1927030     1  0.0672      0.996 0.992 0.008
#&gt; SRR1927028     1  0.0000      0.996 1.000 0.000
#&gt; SRR1927029     2  0.0000      0.998 0.000 1.000
#&gt; SRR1927027     2  0.0672      0.993 0.008 0.992
#&gt; SRR1927026     1  0.0000      0.996 1.000 0.000
#&gt; SRR1927024     1  0.0000      0.996 1.000 0.000
#&gt; SRR1927025     2  0.0672      0.993 0.008 0.992
#&gt; SRR1927023     2  0.0672      0.993 0.008 0.992
#&gt; SRR1927022     1  0.0000      0.996 1.000 0.000
#&gt; SRR1927021     2  0.0000      0.998 0.000 1.000
#&gt; SRR1927020     1  0.0000      0.996 1.000 0.000
#&gt; SRR1927019     2  0.0000      0.998 0.000 1.000
#&gt; SRR1927071     1  0.0000      0.996 1.000 0.000
#&gt; SRR1927069     2  0.0000      0.998 0.000 1.000
#&gt; SRR1927070     1  0.0672      0.996 0.992 0.008
#&gt; SRR1927068     1  0.0000      0.996 1.000 0.000
#&gt; SRR1927066     1  0.0000      0.996 1.000 0.000
#&gt; SRR1927065     2  0.0000      0.998 0.000 1.000
#&gt; SRR1927067     2  0.0000      0.998 0.000 1.000
#&gt; SRR1927064     1  0.0672      0.996 0.992 0.008
#&gt; SRR1927063     2  0.0000      0.998 0.000 1.000
#&gt; SRR1927062     1  0.0000      0.996 1.000 0.000
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-1-a').click(function(){
  $('#tab-SD-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-2'>
<p><a id='tab-SD-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1927048     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927061     3  0.6008      0.692 0.000 0.372 0.628
#&gt; SRR1927060     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927059     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1927058     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927057     2  0.0237      0.994 0.000 0.996 0.004
#&gt; SRR1927055     3  0.2165      0.786 0.000 0.064 0.936
#&gt; SRR1927056     1  0.0424      0.996 0.992 0.000 0.008
#&gt; SRR1927054     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927052     1  0.0424      0.996 0.992 0.000 0.008
#&gt; SRR1927053     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1927051     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1927050     1  0.0424      0.996 0.992 0.000 0.008
#&gt; SRR1927049     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1927047     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1927046     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927045     2  0.0424      0.990 0.000 0.992 0.008
#&gt; SRR1927044     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927043     3  0.5859      0.722 0.000 0.344 0.656
#&gt; SRR1927042     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927039     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1927038     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927037     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1927036     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927035     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1927034     1  0.0424      0.996 0.992 0.000 0.008
#&gt; SRR1927033     3  0.2165      0.786 0.000 0.064 0.936
#&gt; SRR1927032     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927031     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1927030     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927028     1  0.0424      0.996 0.992 0.000 0.008
#&gt; SRR1927029     3  0.5706      0.738 0.000 0.320 0.680
#&gt; SRR1927027     3  0.0000      0.755 0.000 0.000 1.000
#&gt; SRR1927026     1  0.0424      0.996 0.992 0.000 0.008
#&gt; SRR1927024     1  0.0424      0.996 0.992 0.000 0.008
#&gt; SRR1927025     3  0.2537      0.768 0.000 0.080 0.920
#&gt; SRR1927023     3  0.2066      0.762 0.000 0.060 0.940
#&gt; SRR1927022     1  0.0424      0.996 0.992 0.000 0.008
#&gt; SRR1927021     2  0.0424      0.990 0.000 0.992 0.008
#&gt; SRR1927020     1  0.0424      0.996 0.992 0.000 0.008
#&gt; SRR1927019     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1927071     1  0.0424      0.996 0.992 0.000 0.008
#&gt; SRR1927069     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1927070     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927068     1  0.0424      0.996 0.992 0.000 0.008
#&gt; SRR1927066     1  0.0424      0.996 0.992 0.000 0.008
#&gt; SRR1927065     3  0.6062      0.669 0.000 0.384 0.616
#&gt; SRR1927067     3  0.5882      0.721 0.000 0.348 0.652
#&gt; SRR1927064     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927063     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1927062     1  0.0424      0.996 0.992 0.000 0.008
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-2-a').click(function(){
  $('#tab-SD-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-3'>
<p><a id='tab-SD-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1927048     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927061     3  0.4761      0.692 0.000 0.372 0.628 0.000
#&gt; SRR1927060     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1927058     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927057     2  0.0188      0.994 0.000 0.996 0.004 0.000
#&gt; SRR1927055     3  0.1716      0.786 0.000 0.064 0.936 0.000
#&gt; SRR1927056     4  0.0000      0.953 0.000 0.000 0.000 1.000
#&gt; SRR1927054     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927052     4  0.1792      0.953 0.068 0.000 0.000 0.932
#&gt; SRR1927053     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1927051     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1927050     4  0.0000      0.953 0.000 0.000 0.000 1.000
#&gt; SRR1927049     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1927047     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1927046     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927045     2  0.0336      0.990 0.000 0.992 0.008 0.000
#&gt; SRR1927044     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927043     3  0.4643      0.722 0.000 0.344 0.656 0.000
#&gt; SRR1927042     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927039     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1927038     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1927036     1  0.0188      0.996 0.996 0.000 0.000 0.004
#&gt; SRR1927035     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1927034     4  0.0000      0.953 0.000 0.000 0.000 1.000
#&gt; SRR1927033     3  0.1716      0.786 0.000 0.064 0.936 0.000
#&gt; SRR1927032     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927031     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1927030     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927028     4  0.1389      0.963 0.048 0.000 0.000 0.952
#&gt; SRR1927029     3  0.4522      0.738 0.000 0.320 0.680 0.000
#&gt; SRR1927027     3  0.0000      0.750 0.000 0.000 1.000 0.000
#&gt; SRR1927026     4  0.1211      0.962 0.040 0.000 0.000 0.960
#&gt; SRR1927024     4  0.1637      0.956 0.060 0.000 0.000 0.940
#&gt; SRR1927025     3  0.2011      0.768 0.000 0.080 0.920 0.000
#&gt; SRR1927023     3  0.1637      0.762 0.000 0.060 0.940 0.000
#&gt; SRR1927022     4  0.2921      0.879 0.140 0.000 0.000 0.860
#&gt; SRR1927021     2  0.0336      0.990 0.000 0.992 0.008 0.000
#&gt; SRR1927020     4  0.0000      0.953 0.000 0.000 0.000 1.000
#&gt; SRR1927019     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1927071     4  0.1389      0.963 0.048 0.000 0.000 0.952
#&gt; SRR1927069     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1927070     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927068     4  0.0000      0.953 0.000 0.000 0.000 1.000
#&gt; SRR1927066     4  0.1557      0.960 0.056 0.000 0.000 0.944
#&gt; SRR1927065     3  0.4804      0.669 0.000 0.384 0.616 0.000
#&gt; SRR1927067     3  0.4661      0.721 0.000 0.348 0.652 0.000
#&gt; SRR1927064     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927063     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1927062     4  0.1557      0.960 0.056 0.000 0.000 0.944
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-3-a').click(function(){
  $('#tab-SD-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-4'>
<p><a id='tab-SD-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1927048     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927061     3  0.3966      0.782 0.000 0.336 0.664 0.000 0.000
#&gt; SRR1927060     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927058     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927057     2  0.0162      0.989 0.000 0.996 0.004 0.000 0.000
#&gt; SRR1927055     3  0.0000      0.504 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927056     4  0.0000      0.945 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927054     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927052     4  0.1544      0.945 0.068 0.000 0.000 0.932 0.000
#&gt; SRR1927053     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927051     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927050     4  0.0000      0.945 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927049     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927047     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927046     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927045     2  0.0290      0.985 0.000 0.992 0.008 0.000 0.000
#&gt; SRR1927044     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927043     3  0.3707      0.800 0.000 0.284 0.716 0.000 0.000
#&gt; SRR1927042     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927039     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927038     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927036     1  0.0162      0.995 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1927035     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927034     4  0.0000      0.945 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927033     3  0.0000      0.504 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927032     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927031     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927030     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927028     4  0.1197      0.956 0.048 0.000 0.000 0.952 0.000
#&gt; SRR1927029     3  0.3534      0.792 0.000 0.256 0.744 0.000 0.000
#&gt; SRR1927027     5  0.3913      0.705 0.000 0.000 0.324 0.000 0.676
#&gt; SRR1927026     4  0.1043      0.956 0.040 0.000 0.000 0.960 0.000
#&gt; SRR1927024     4  0.1410      0.949 0.060 0.000 0.000 0.940 0.000
#&gt; SRR1927025     5  0.0609      0.853 0.000 0.020 0.000 0.000 0.980
#&gt; SRR1927023     5  0.0000      0.857 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1927022     4  0.2516      0.857 0.140 0.000 0.000 0.860 0.000
#&gt; SRR1927021     2  0.1544      0.915 0.000 0.932 0.000 0.000 0.068
#&gt; SRR1927020     4  0.0000      0.945 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927019     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927071     4  0.1197      0.956 0.048 0.000 0.000 0.952 0.000
#&gt; SRR1927069     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927070     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927068     4  0.0000      0.945 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927066     4  0.1341      0.954 0.056 0.000 0.000 0.944 0.000
#&gt; SRR1927065     3  0.3999      0.771 0.000 0.344 0.656 0.000 0.000
#&gt; SRR1927067     3  0.3857      0.795 0.000 0.312 0.688 0.000 0.000
#&gt; SRR1927064     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927063     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927062     4  0.1341      0.954 0.056 0.000 0.000 0.944 0.000
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-4-a').click(function(){
  $('#tab-SD-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-5'>
<p><a id='tab-SD-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1927048     1  0.0000      0.999 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927061     3  0.1856      0.836 0.000 0.048 0.920 0.000 0.000 0.032
#&gt; SRR1927060     1  0.0000      0.999 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.0000      0.986 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927058     1  0.0000      0.999 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927057     2  0.1334      0.948 0.000 0.948 0.020 0.000 0.000 0.032
#&gt; SRR1927055     3  0.3198      0.673 0.000 0.000 0.740 0.000 0.000 0.260
#&gt; SRR1927056     4  0.0260      0.947 0.000 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1927054     1  0.0000      0.999 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927052     4  0.1267      0.945 0.060 0.000 0.000 0.940 0.000 0.000
#&gt; SRR1927053     2  0.0000      0.986 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927051     2  0.0000      0.986 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927050     4  0.0260      0.947 0.000 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1927049     2  0.0000      0.986 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927047     2  0.0000      0.986 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927046     1  0.0260      0.991 0.992 0.000 0.000 0.008 0.000 0.000
#&gt; SRR1927045     2  0.0713      0.966 0.000 0.972 0.028 0.000 0.000 0.000
#&gt; SRR1927044     1  0.0000      0.999 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927043     3  0.0632      0.849 0.000 0.024 0.976 0.000 0.000 0.000
#&gt; SRR1927042     1  0.0000      0.999 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      0.999 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927039     2  0.0000      0.986 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927038     1  0.0000      0.999 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.0000      0.986 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927036     1  0.0146      0.995 0.996 0.000 0.000 0.004 0.000 0.000
#&gt; SRR1927035     2  0.0000      0.986 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927034     4  0.0260      0.947 0.000 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1927033     3  0.3198      0.673 0.000 0.000 0.740 0.000 0.000 0.260
#&gt; SRR1927032     1  0.0000      0.999 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927031     2  0.0000      0.986 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927030     1  0.0000      0.999 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927028     4  0.0937      0.957 0.040 0.000 0.000 0.960 0.000 0.000
#&gt; SRR1927029     3  0.0146      0.837 0.000 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1927027     6  0.1007      0.000 0.000 0.000 0.000 0.000 0.044 0.956
#&gt; SRR1927026     4  0.0790      0.956 0.032 0.000 0.000 0.968 0.000 0.000
#&gt; SRR1927024     4  0.1141      0.949 0.052 0.000 0.000 0.948 0.000 0.000
#&gt; SRR1927025     5  0.0547      0.954 0.000 0.020 0.000 0.000 0.980 0.000
#&gt; SRR1927023     5  0.0000      0.953 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927022     4  0.2178      0.852 0.132 0.000 0.000 0.868 0.000 0.000
#&gt; SRR1927021     2  0.1387      0.927 0.000 0.932 0.000 0.000 0.068 0.000
#&gt; SRR1927020     4  0.0260      0.947 0.000 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1927019     2  0.0000      0.986 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927071     4  0.0937      0.957 0.040 0.000 0.000 0.960 0.000 0.000
#&gt; SRR1927069     2  0.0000      0.986 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927070     1  0.0000      0.999 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927068     4  0.0260      0.947 0.000 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1927066     4  0.1075      0.954 0.048 0.000 0.000 0.952 0.000 0.000
#&gt; SRR1927065     3  0.2039      0.810 0.000 0.076 0.904 0.000 0.000 0.020
#&gt; SRR1927067     3  0.1418      0.844 0.000 0.024 0.944 0.000 0.000 0.032
#&gt; SRR1927064     1  0.0000      0.999 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927063     2  0.0891      0.964 0.000 0.968 0.008 0.000 0.000 0.024
#&gt; SRR1927062     4  0.1075      0.954 0.048 0.000 0.000 0.952 0.000 0.000
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-5-a').click(function(){
  $('#tab-SD-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-SD-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-signatures'>
<ul>
<li><a href='#tab-SD-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-1-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-1"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-2-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-2"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-3-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-3"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-4-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-4"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-5-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-hclust-signature_compare](figure_cola/SD-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-SD-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-hclust-collect-classes](figure_cola/SD-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:kmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "kmeans"]
# you can also extract it by
# res = res_list["SD:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16868 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-kmeans-collect-plots](figure_cola/SD-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-kmeans-select-partition-number](figure_cola/SD-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5095 0.491   0.491
#> 3 3 0.742           0.881       0.807         0.2476 0.864   0.724
#> 4 4 0.680           0.911       0.861         0.1286 0.872   0.648
#> 5 5 0.802           0.781       0.841         0.0682 0.994   0.975
#> 6 6 0.832           0.662       0.786         0.0449 0.985   0.937
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-classes'>
<ul>
<li><a href='#tab-SD-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-kmeans-get-classes-1'>
<p><a id='tab-SD-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1927048     1       0          1  1  0
#&gt; SRR1927061     2       0          1  0  1
#&gt; SRR1927060     1       0          1  1  0
#&gt; SRR1927059     2       0          1  0  1
#&gt; SRR1927058     1       0          1  1  0
#&gt; SRR1927057     2       0          1  0  1
#&gt; SRR1927055     2       0          1  0  1
#&gt; SRR1927056     1       0          1  1  0
#&gt; SRR1927054     1       0          1  1  0
#&gt; SRR1927052     1       0          1  1  0
#&gt; SRR1927053     2       0          1  0  1
#&gt; SRR1927051     2       0          1  0  1
#&gt; SRR1927050     1       0          1  1  0
#&gt; SRR1927049     2       0          1  0  1
#&gt; SRR1927047     2       0          1  0  1
#&gt; SRR1927046     1       0          1  1  0
#&gt; SRR1927045     2       0          1  0  1
#&gt; SRR1927044     1       0          1  1  0
#&gt; SRR1927043     2       0          1  0  1
#&gt; SRR1927042     1       0          1  1  0
#&gt; SRR1927040     1       0          1  1  0
#&gt; SRR1927039     2       0          1  0  1
#&gt; SRR1927038     1       0          1  1  0
#&gt; SRR1927037     2       0          1  0  1
#&gt; SRR1927036     1       0          1  1  0
#&gt; SRR1927035     2       0          1  0  1
#&gt; SRR1927034     1       0          1  1  0
#&gt; SRR1927033     2       0          1  0  1
#&gt; SRR1927032     1       0          1  1  0
#&gt; SRR1927031     2       0          1  0  1
#&gt; SRR1927030     1       0          1  1  0
#&gt; SRR1927028     1       0          1  1  0
#&gt; SRR1927029     2       0          1  0  1
#&gt; SRR1927027     2       0          1  0  1
#&gt; SRR1927026     1       0          1  1  0
#&gt; SRR1927024     1       0          1  1  0
#&gt; SRR1927025     2       0          1  0  1
#&gt; SRR1927023     2       0          1  0  1
#&gt; SRR1927022     1       0          1  1  0
#&gt; SRR1927021     2       0          1  0  1
#&gt; SRR1927020     1       0          1  1  0
#&gt; SRR1927019     2       0          1  0  1
#&gt; SRR1927071     1       0          1  1  0
#&gt; SRR1927069     2       0          1  0  1
#&gt; SRR1927070     1       0          1  1  0
#&gt; SRR1927068     1       0          1  1  0
#&gt; SRR1927066     1       0          1  1  0
#&gt; SRR1927065     2       0          1  0  1
#&gt; SRR1927067     2       0          1  0  1
#&gt; SRR1927064     1       0          1  1  0
#&gt; SRR1927063     2       0          1  0  1
#&gt; SRR1927062     1       0          1  1  0
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-1-a').click(function(){
  $('#tab-SD-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-2'>
<p><a id='tab-SD-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1927048     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR1927061     2  0.0892      0.717 0.000 0.980 0.020
#&gt; SRR1927060     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR1927059     2  0.6267      0.849 0.000 0.548 0.452
#&gt; SRR1927058     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR1927057     2  0.6267      0.849 0.000 0.548 0.452
#&gt; SRR1927055     2  0.0237      0.707 0.000 0.996 0.004
#&gt; SRR1927056     3  0.6274      1.000 0.456 0.000 0.544
#&gt; SRR1927054     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR1927052     3  0.6274      1.000 0.456 0.000 0.544
#&gt; SRR1927053     2  0.6267      0.849 0.000 0.548 0.452
#&gt; SRR1927051     2  0.6267      0.849 0.000 0.548 0.452
#&gt; SRR1927050     3  0.6274      1.000 0.456 0.000 0.544
#&gt; SRR1927049     2  0.6267      0.849 0.000 0.548 0.452
#&gt; SRR1927047     2  0.6267      0.849 0.000 0.548 0.452
#&gt; SRR1927046     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR1927045     2  0.6267      0.849 0.000 0.548 0.452
#&gt; SRR1927044     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR1927043     2  0.0000      0.709 0.000 1.000 0.000
#&gt; SRR1927042     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR1927039     2  0.6267      0.849 0.000 0.548 0.452
#&gt; SRR1927038     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR1927037     2  0.6267      0.849 0.000 0.548 0.452
#&gt; SRR1927036     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR1927035     2  0.6267      0.849 0.000 0.548 0.452
#&gt; SRR1927034     3  0.6274      1.000 0.456 0.000 0.544
#&gt; SRR1927033     2  0.0237      0.707 0.000 0.996 0.004
#&gt; SRR1927032     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR1927031     2  0.6267      0.849 0.000 0.548 0.452
#&gt; SRR1927030     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR1927028     3  0.6274      1.000 0.456 0.000 0.544
#&gt; SRR1927029     2  0.0000      0.709 0.000 1.000 0.000
#&gt; SRR1927027     2  0.5785      0.202 0.000 0.668 0.332
#&gt; SRR1927026     3  0.6274      1.000 0.456 0.000 0.544
#&gt; SRR1927024     3  0.6274      1.000 0.456 0.000 0.544
#&gt; SRR1927025     2  0.5810      0.818 0.000 0.664 0.336
#&gt; SRR1927023     2  0.2959      0.744 0.000 0.900 0.100
#&gt; SRR1927022     1  0.3879      0.617 0.848 0.000 0.152
#&gt; SRR1927021     2  0.6267      0.849 0.000 0.548 0.452
#&gt; SRR1927020     3  0.6274      1.000 0.456 0.000 0.544
#&gt; SRR1927019     2  0.6267      0.849 0.000 0.548 0.452
#&gt; SRR1927071     3  0.6274      1.000 0.456 0.000 0.544
#&gt; SRR1927069     2  0.6267      0.849 0.000 0.548 0.452
#&gt; SRR1927070     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR1927068     3  0.6274      1.000 0.456 0.000 0.544
#&gt; SRR1927066     3  0.6274      1.000 0.456 0.000 0.544
#&gt; SRR1927065     2  0.0000      0.709 0.000 1.000 0.000
#&gt; SRR1927067     2  0.0000      0.709 0.000 1.000 0.000
#&gt; SRR1927064     1  0.0000      0.980 1.000 0.000 0.000
#&gt; SRR1927063     2  0.6267      0.849 0.000 0.548 0.452
#&gt; SRR1927062     3  0.6274      1.000 0.456 0.000 0.544
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-2-a').click(function(){
  $('#tab-SD-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-3'>
<p><a id='tab-SD-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1927048     1  0.4990      0.947 0.756 0.000 0.060 0.184
#&gt; SRR1927061     3  0.4608      0.867 0.004 0.304 0.692 0.000
#&gt; SRR1927060     1  0.3444      0.953 0.816 0.000 0.000 0.184
#&gt; SRR1927059     2  0.0707      0.962 0.020 0.980 0.000 0.000
#&gt; SRR1927058     1  0.3444      0.953 0.816 0.000 0.000 0.184
#&gt; SRR1927057     2  0.0592      0.962 0.016 0.984 0.000 0.000
#&gt; SRR1927055     3  0.5218      0.855 0.064 0.200 0.736 0.000
#&gt; SRR1927056     4  0.2647      0.905 0.000 0.000 0.120 0.880
#&gt; SRR1927054     1  0.3444      0.953 0.816 0.000 0.000 0.184
#&gt; SRR1927052     4  0.1716      0.893 0.000 0.000 0.064 0.936
#&gt; SRR1927053     2  0.0707      0.962 0.020 0.980 0.000 0.000
#&gt; SRR1927051     2  0.0188      0.964 0.004 0.996 0.000 0.000
#&gt; SRR1927050     4  0.2647      0.905 0.000 0.000 0.120 0.880
#&gt; SRR1927049     2  0.0188      0.964 0.004 0.996 0.000 0.000
#&gt; SRR1927047     2  0.0336      0.963 0.008 0.992 0.000 0.000
#&gt; SRR1927046     1  0.5633      0.935 0.716 0.000 0.100 0.184
#&gt; SRR1927045     2  0.0188      0.964 0.004 0.996 0.000 0.000
#&gt; SRR1927044     1  0.5798      0.930 0.704 0.000 0.112 0.184
#&gt; SRR1927043     3  0.4343      0.898 0.004 0.264 0.732 0.000
#&gt; SRR1927042     1  0.3444      0.953 0.816 0.000 0.000 0.184
#&gt; SRR1927040     1  0.3444      0.953 0.816 0.000 0.000 0.184
#&gt; SRR1927039     2  0.0707      0.962 0.020 0.980 0.000 0.000
#&gt; SRR1927038     1  0.3444      0.953 0.816 0.000 0.000 0.184
#&gt; SRR1927037     2  0.0469      0.963 0.012 0.988 0.000 0.000
#&gt; SRR1927036     1  0.5798      0.930 0.704 0.000 0.112 0.184
#&gt; SRR1927035     2  0.0000      0.964 0.000 1.000 0.000 0.000
#&gt; SRR1927034     4  0.2647      0.905 0.000 0.000 0.120 0.880
#&gt; SRR1927033     3  0.5648      0.883 0.064 0.252 0.684 0.000
#&gt; SRR1927032     1  0.3444      0.953 0.816 0.000 0.000 0.184
#&gt; SRR1927031     2  0.0707      0.962 0.020 0.980 0.000 0.000
#&gt; SRR1927030     1  0.5798      0.930 0.704 0.000 0.112 0.184
#&gt; SRR1927028     4  0.0000      0.922 0.000 0.000 0.000 1.000
#&gt; SRR1927029     3  0.4164      0.899 0.000 0.264 0.736 0.000
#&gt; SRR1927027     3  0.6847      0.737 0.148 0.112 0.684 0.056
#&gt; SRR1927026     4  0.0188      0.922 0.000 0.000 0.004 0.996
#&gt; SRR1927024     4  0.0469      0.921 0.000 0.000 0.012 0.988
#&gt; SRR1927025     2  0.5650      0.462 0.104 0.716 0.180 0.000
#&gt; SRR1927023     3  0.7363      0.701 0.168 0.356 0.476 0.000
#&gt; SRR1927022     4  0.4869      0.705 0.088 0.000 0.132 0.780
#&gt; SRR1927021     2  0.0707      0.957 0.020 0.980 0.000 0.000
#&gt; SRR1927020     4  0.2647      0.905 0.000 0.000 0.120 0.880
#&gt; SRR1927019     2  0.0188      0.964 0.004 0.996 0.000 0.000
#&gt; SRR1927071     4  0.0188      0.921 0.000 0.000 0.004 0.996
#&gt; SRR1927069     2  0.0336      0.963 0.008 0.992 0.000 0.000
#&gt; SRR1927070     1  0.5798      0.930 0.704 0.000 0.112 0.184
#&gt; SRR1927068     4  0.2647      0.905 0.000 0.000 0.120 0.880
#&gt; SRR1927066     4  0.0921      0.915 0.000 0.000 0.028 0.972
#&gt; SRR1927065     3  0.4372      0.897 0.004 0.268 0.728 0.000
#&gt; SRR1927067     3  0.4164      0.899 0.000 0.264 0.736 0.000
#&gt; SRR1927064     1  0.4679      0.949 0.772 0.000 0.044 0.184
#&gt; SRR1927063     2  0.0188      0.964 0.004 0.996 0.000 0.000
#&gt; SRR1927062     4  0.0921      0.915 0.000 0.000 0.028 0.972
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-3-a').click(function(){
  $('#tab-SD-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-4'>
<p><a id='tab-SD-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1927048     1  0.2735     0.8960 0.880 0.000 0.036 0.000 0.084
#&gt; SRR1927061     3  0.3048     0.6373 0.000 0.176 0.820 0.004 0.000
#&gt; SRR1927060     1  0.1357     0.8938 0.948 0.000 0.048 0.000 0.004
#&gt; SRR1927059     2  0.1830     0.9204 0.000 0.932 0.000 0.028 0.040
#&gt; SRR1927058     1  0.0671     0.9008 0.980 0.000 0.016 0.000 0.004
#&gt; SRR1927057     2  0.1911     0.9207 0.000 0.932 0.004 0.028 0.036
#&gt; SRR1927055     3  0.4787     0.4524 0.000 0.080 0.712 0.000 0.208
#&gt; SRR1927056     4  0.5368     0.7622 0.072 0.000 0.000 0.596 0.332
#&gt; SRR1927054     1  0.1357     0.8938 0.948 0.000 0.048 0.000 0.004
#&gt; SRR1927052     4  0.2473     0.8260 0.072 0.000 0.000 0.896 0.032
#&gt; SRR1927053     2  0.1830     0.9204 0.000 0.932 0.000 0.028 0.040
#&gt; SRR1927051     2  0.0162     0.9284 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1927050     4  0.5368     0.7622 0.072 0.000 0.000 0.596 0.332
#&gt; SRR1927049     2  0.0162     0.9284 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1927047     2  0.0955     0.9278 0.000 0.968 0.000 0.004 0.028
#&gt; SRR1927046     1  0.3844     0.8722 0.792 0.000 0.044 0.000 0.164
#&gt; SRR1927045     2  0.0693     0.9216 0.000 0.980 0.012 0.008 0.000
#&gt; SRR1927044     1  0.3535     0.8763 0.808 0.000 0.028 0.000 0.164
#&gt; SRR1927043     3  0.2329     0.7191 0.000 0.124 0.876 0.000 0.000
#&gt; SRR1927042     1  0.0451     0.9037 0.988 0.000 0.008 0.000 0.004
#&gt; SRR1927040     1  0.1357     0.8938 0.948 0.000 0.048 0.000 0.004
#&gt; SRR1927039     2  0.1830     0.9204 0.000 0.932 0.000 0.028 0.040
#&gt; SRR1927038     1  0.1357     0.8938 0.948 0.000 0.048 0.000 0.004
#&gt; SRR1927037     2  0.1661     0.9210 0.000 0.940 0.000 0.024 0.036
#&gt; SRR1927036     1  0.3612     0.8738 0.800 0.000 0.028 0.000 0.172
#&gt; SRR1927035     2  0.0000     0.9288 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927034     4  0.5368     0.7622 0.072 0.000 0.000 0.596 0.332
#&gt; SRR1927033     3  0.4914     0.4869 0.000 0.108 0.712 0.000 0.180
#&gt; SRR1927032     1  0.0579     0.9018 0.984 0.000 0.008 0.000 0.008
#&gt; SRR1927031     2  0.1830     0.9204 0.000 0.932 0.000 0.028 0.040
#&gt; SRR1927030     1  0.3612     0.8738 0.800 0.000 0.028 0.000 0.172
#&gt; SRR1927028     4  0.1608     0.8309 0.072 0.000 0.000 0.928 0.000
#&gt; SRR1927029     3  0.2329     0.7191 0.000 0.124 0.876 0.000 0.000
#&gt; SRR1927027     3  0.5551    -0.4024 0.000 0.068 0.488 0.000 0.444
#&gt; SRR1927026     4  0.2507     0.8281 0.072 0.000 0.016 0.900 0.012
#&gt; SRR1927024     4  0.2611     0.8270 0.072 0.000 0.016 0.896 0.016
#&gt; SRR1927025     2  0.6557     0.0736 0.000 0.588 0.128 0.044 0.240
#&gt; SRR1927023     5  0.7294     0.0000 0.000 0.196 0.376 0.036 0.392
#&gt; SRR1927022     4  0.5881     0.6178 0.140 0.000 0.020 0.652 0.188
#&gt; SRR1927021     2  0.1310     0.9094 0.000 0.956 0.000 0.020 0.024
#&gt; SRR1927020     4  0.5368     0.7622 0.072 0.000 0.000 0.596 0.332
#&gt; SRR1927019     2  0.0162     0.9284 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1927071     4  0.1608     0.8309 0.072 0.000 0.000 0.928 0.000
#&gt; SRR1927069     2  0.0451     0.9276 0.000 0.988 0.000 0.008 0.004
#&gt; SRR1927070     1  0.3574     0.8745 0.804 0.000 0.028 0.000 0.168
#&gt; SRR1927068     4  0.5368     0.7622 0.072 0.000 0.000 0.596 0.332
#&gt; SRR1927066     4  0.2473     0.8260 0.072 0.000 0.000 0.896 0.032
#&gt; SRR1927065     3  0.2648     0.6916 0.000 0.152 0.848 0.000 0.000
#&gt; SRR1927067     3  0.2329     0.7191 0.000 0.124 0.876 0.000 0.000
#&gt; SRR1927064     1  0.2409     0.8990 0.900 0.000 0.032 0.000 0.068
#&gt; SRR1927063     2  0.0324     0.9272 0.000 0.992 0.004 0.004 0.000
#&gt; SRR1927062     4  0.2473     0.8260 0.072 0.000 0.000 0.896 0.032
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-4-a').click(function(){
  $('#tab-SD-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-5'>
<p><a id='tab-SD-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1927048     1  0.4284     0.7432 0.748 0.000 0.008 0.000 0.136 0.108
#&gt; SRR1927061     3  0.2504     0.7131 0.000 0.088 0.880 0.004 0.000 0.028
#&gt; SRR1927060     1  0.2056     0.7588 0.904 0.000 0.004 0.000 0.080 0.012
#&gt; SRR1927059     2  0.3395     0.8384 0.000 0.808 0.000 0.000 0.060 0.132
#&gt; SRR1927058     1  0.1524     0.7716 0.932 0.000 0.000 0.000 0.060 0.008
#&gt; SRR1927057     2  0.3447     0.8394 0.000 0.804 0.000 0.004 0.044 0.148
#&gt; SRR1927055     3  0.5539     0.3715 0.000 0.024 0.688 0.052 0.156 0.080
#&gt; SRR1927056     4  0.1141     0.5202 0.052 0.000 0.000 0.948 0.000 0.000
#&gt; SRR1927054     1  0.2056     0.7588 0.904 0.000 0.004 0.000 0.080 0.012
#&gt; SRR1927052     4  0.4806     0.3833 0.052 0.000 0.000 0.488 0.000 0.460
#&gt; SRR1927053     2  0.3395     0.8384 0.000 0.808 0.000 0.000 0.060 0.132
#&gt; SRR1927051     2  0.0858     0.8632 0.000 0.968 0.004 0.000 0.000 0.028
#&gt; SRR1927050     4  0.1969     0.5097 0.052 0.000 0.004 0.920 0.020 0.004
#&gt; SRR1927049     2  0.0858     0.8632 0.000 0.968 0.004 0.000 0.000 0.028
#&gt; SRR1927047     2  0.1624     0.8649 0.000 0.936 0.000 0.004 0.040 0.020
#&gt; SRR1927046     1  0.5059     0.6803 0.628 0.000 0.000 0.000 0.140 0.232
#&gt; SRR1927045     2  0.1296     0.8588 0.000 0.948 0.004 0.004 0.000 0.044
#&gt; SRR1927044     1  0.4484     0.7047 0.672 0.000 0.004 0.000 0.056 0.268
#&gt; SRR1927043     3  0.1007     0.7886 0.000 0.044 0.956 0.000 0.000 0.000
#&gt; SRR1927042     1  0.1478     0.7831 0.944 0.000 0.004 0.000 0.020 0.032
#&gt; SRR1927040     1  0.2056     0.7588 0.904 0.000 0.004 0.000 0.080 0.012
#&gt; SRR1927039     2  0.3395     0.8384 0.000 0.808 0.000 0.000 0.060 0.132
#&gt; SRR1927038     1  0.2056     0.7588 0.904 0.000 0.004 0.000 0.080 0.012
#&gt; SRR1927037     2  0.3130     0.8406 0.000 0.828 0.000 0.000 0.048 0.124
#&gt; SRR1927036     1  0.4505     0.7021 0.668 0.000 0.004 0.000 0.056 0.272
#&gt; SRR1927035     2  0.0146     0.8665 0.000 0.996 0.004 0.000 0.000 0.000
#&gt; SRR1927034     4  0.1969     0.5097 0.052 0.000 0.004 0.920 0.020 0.004
#&gt; SRR1927033     3  0.5568     0.3962 0.000 0.036 0.688 0.040 0.156 0.080
#&gt; SRR1927032     1  0.1398     0.7784 0.940 0.000 0.008 0.000 0.052 0.000
#&gt; SRR1927031     2  0.3354     0.8391 0.000 0.812 0.000 0.000 0.060 0.128
#&gt; SRR1927030     1  0.4505     0.7021 0.668 0.000 0.004 0.000 0.056 0.272
#&gt; SRR1927028     4  0.4763     0.4713 0.052 0.000 0.000 0.536 0.000 0.412
#&gt; SRR1927029     3  0.0865     0.7886 0.000 0.036 0.964 0.000 0.000 0.000
#&gt; SRR1927027     5  0.6564     0.5836 0.000 0.024 0.380 0.052 0.460 0.084
#&gt; SRR1927026     4  0.6151     0.3585 0.052 0.000 0.012 0.480 0.064 0.392
#&gt; SRR1927024     4  0.6270     0.3445 0.052 0.000 0.016 0.476 0.068 0.388
#&gt; SRR1927025     2  0.5837    -0.0585 0.000 0.444 0.084 0.008 0.444 0.020
#&gt; SRR1927023     5  0.4700     0.6527 0.000 0.076 0.288 0.000 0.636 0.000
#&gt; SRR1927022     6  0.5882     0.0000 0.088 0.000 0.016 0.196 0.060 0.640
#&gt; SRR1927021     2  0.2465     0.8335 0.000 0.892 0.004 0.008 0.072 0.024
#&gt; SRR1927020     4  0.1141     0.5202 0.052 0.000 0.000 0.948 0.000 0.000
#&gt; SRR1927019     2  0.1080     0.8621 0.000 0.960 0.004 0.004 0.000 0.032
#&gt; SRR1927071     4  0.4768     0.4692 0.052 0.000 0.000 0.532 0.000 0.416
#&gt; SRR1927069     2  0.1476     0.8608 0.000 0.948 0.004 0.008 0.012 0.028
#&gt; SRR1927070     1  0.4505     0.7021 0.668 0.000 0.004 0.000 0.056 0.272
#&gt; SRR1927068     4  0.1141     0.5202 0.052 0.000 0.000 0.948 0.000 0.000
#&gt; SRR1927066     4  0.4787     0.4481 0.052 0.000 0.000 0.516 0.000 0.432
#&gt; SRR1927065     3  0.1829     0.7672 0.000 0.064 0.920 0.004 0.000 0.012
#&gt; SRR1927067     3  0.0865     0.7886 0.000 0.036 0.964 0.000 0.000 0.000
#&gt; SRR1927064     1  0.3587     0.7573 0.804 0.000 0.008 0.000 0.132 0.056
#&gt; SRR1927063     2  0.1155     0.8611 0.000 0.956 0.004 0.004 0.000 0.036
#&gt; SRR1927062     4  0.4778     0.4533 0.052 0.000 0.000 0.524 0.000 0.424
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-5-a').click(function(){
  $('#tab-SD-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-SD-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-signatures'>
<ul>
<li><a href='#tab-SD-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-kmeans-signature_compare](figure_cola/SD-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-SD-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-kmeans-collect-classes](figure_cola/SD-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:skmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "skmeans"]
# you can also extract it by
# res = res_list["SD:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16868 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 5.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-skmeans-collect-plots](figure_cola/SD-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-skmeans-select-partition-number](figure_cola/SD-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5095 0.491   0.491
#> 3 3 1.000           0.963       0.983         0.2771 0.835   0.670
#> 4 4 1.000           0.975       0.990         0.1545 0.895   0.701
#> 5 5 1.000           0.980       0.988         0.0323 0.971   0.884
#> 6 6 0.904           0.857       0.919         0.0253 0.998   0.993
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 5
#> attr(,"optional")
#> [1] 2 3 4
```

There is also optional best $k$ = 2 3 4 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-classes'>
<ul>
<li><a href='#tab-SD-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-skmeans-get-classes-1'>
<p><a id='tab-SD-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1927048     1       0          1  1  0
#&gt; SRR1927061     2       0          1  0  1
#&gt; SRR1927060     1       0          1  1  0
#&gt; SRR1927059     2       0          1  0  1
#&gt; SRR1927058     1       0          1  1  0
#&gt; SRR1927057     2       0          1  0  1
#&gt; SRR1927055     2       0          1  0  1
#&gt; SRR1927056     1       0          1  1  0
#&gt; SRR1927054     1       0          1  1  0
#&gt; SRR1927052     1       0          1  1  0
#&gt; SRR1927053     2       0          1  0  1
#&gt; SRR1927051     2       0          1  0  1
#&gt; SRR1927050     1       0          1  1  0
#&gt; SRR1927049     2       0          1  0  1
#&gt; SRR1927047     2       0          1  0  1
#&gt; SRR1927046     1       0          1  1  0
#&gt; SRR1927045     2       0          1  0  1
#&gt; SRR1927044     1       0          1  1  0
#&gt; SRR1927043     2       0          1  0  1
#&gt; SRR1927042     1       0          1  1  0
#&gt; SRR1927040     1       0          1  1  0
#&gt; SRR1927039     2       0          1  0  1
#&gt; SRR1927038     1       0          1  1  0
#&gt; SRR1927037     2       0          1  0  1
#&gt; SRR1927036     1       0          1  1  0
#&gt; SRR1927035     2       0          1  0  1
#&gt; SRR1927034     1       0          1  1  0
#&gt; SRR1927033     2       0          1  0  1
#&gt; SRR1927032     1       0          1  1  0
#&gt; SRR1927031     2       0          1  0  1
#&gt; SRR1927030     1       0          1  1  0
#&gt; SRR1927028     1       0          1  1  0
#&gt; SRR1927029     2       0          1  0  1
#&gt; SRR1927027     2       0          1  0  1
#&gt; SRR1927026     1       0          1  1  0
#&gt; SRR1927024     1       0          1  1  0
#&gt; SRR1927025     2       0          1  0  1
#&gt; SRR1927023     2       0          1  0  1
#&gt; SRR1927022     1       0          1  1  0
#&gt; SRR1927021     2       0          1  0  1
#&gt; SRR1927020     1       0          1  1  0
#&gt; SRR1927019     2       0          1  0  1
#&gt; SRR1927071     1       0          1  1  0
#&gt; SRR1927069     2       0          1  0  1
#&gt; SRR1927070     1       0          1  1  0
#&gt; SRR1927068     1       0          1  1  0
#&gt; SRR1927066     1       0          1  1  0
#&gt; SRR1927065     2       0          1  0  1
#&gt; SRR1927067     2       0          1  0  1
#&gt; SRR1927064     1       0          1  1  0
#&gt; SRR1927063     2       0          1  0  1
#&gt; SRR1927062     1       0          1  1  0
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-1-a').click(function(){
  $('#tab-SD-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-2'>
<p><a id='tab-SD-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1927048     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927061     2  0.0592      0.992 0.000 0.988 0.012
#&gt; SRR1927060     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927059     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927058     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927057     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927055     2  0.0592      0.992 0.000 0.988 0.012
#&gt; SRR1927056     3  0.0592      0.941 0.012 0.000 0.988
#&gt; SRR1927054     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927052     3  0.0592      0.941 0.012 0.000 0.988
#&gt; SRR1927053     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927051     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927050     3  0.0592      0.941 0.012 0.000 0.988
#&gt; SRR1927049     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927047     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927046     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927045     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927044     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927043     2  0.0592      0.992 0.000 0.988 0.012
#&gt; SRR1927042     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927039     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927038     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927037     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927036     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927035     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927034     3  0.0592      0.941 0.012 0.000 0.988
#&gt; SRR1927033     2  0.0592      0.992 0.000 0.988 0.012
#&gt; SRR1927032     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927031     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927030     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927028     3  0.0592      0.941 0.012 0.000 0.988
#&gt; SRR1927029     2  0.0592      0.992 0.000 0.988 0.012
#&gt; SRR1927027     3  0.6180      0.266 0.000 0.416 0.584
#&gt; SRR1927026     3  0.0592      0.941 0.012 0.000 0.988
#&gt; SRR1927024     3  0.0592      0.941 0.012 0.000 0.988
#&gt; SRR1927025     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927023     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927022     3  0.5216      0.641 0.260 0.000 0.740
#&gt; SRR1927021     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927020     3  0.0592      0.941 0.012 0.000 0.988
#&gt; SRR1927019     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927071     3  0.0592      0.941 0.012 0.000 0.988
#&gt; SRR1927069     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927070     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927068     3  0.0592      0.941 0.012 0.000 0.988
#&gt; SRR1927066     3  0.0592      0.941 0.012 0.000 0.988
#&gt; SRR1927065     2  0.0592      0.992 0.000 0.988 0.012
#&gt; SRR1927067     2  0.0592      0.992 0.000 0.988 0.012
#&gt; SRR1927064     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927063     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927062     3  0.0592      0.941 0.012 0.000 0.988
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-2-a').click(function(){
  $('#tab-SD-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-3'>
<p><a id='tab-SD-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1927048     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927061     3  0.0188      0.996 0.000 0.004 0.996 0.000
#&gt; SRR1927060     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR1927058     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927057     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR1927055     3  0.0000      0.999 0.000 0.000 1.000 0.000
#&gt; SRR1927056     4  0.0000      0.989 0.000 0.000 0.000 1.000
#&gt; SRR1927054     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927052     4  0.0000      0.989 0.000 0.000 0.000 1.000
#&gt; SRR1927053     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR1927051     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR1927050     4  0.0000      0.989 0.000 0.000 0.000 1.000
#&gt; SRR1927049     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR1927047     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR1927046     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927045     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR1927044     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927043     3  0.0000      0.999 0.000 0.000 1.000 0.000
#&gt; SRR1927042     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927039     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR1927038     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR1927036     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927035     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR1927034     4  0.0000      0.989 0.000 0.000 0.000 1.000
#&gt; SRR1927033     3  0.0000      0.999 0.000 0.000 1.000 0.000
#&gt; SRR1927032     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927031     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR1927030     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927028     4  0.0000      0.989 0.000 0.000 0.000 1.000
#&gt; SRR1927029     3  0.0000      0.999 0.000 0.000 1.000 0.000
#&gt; SRR1927027     3  0.0000      0.999 0.000 0.000 1.000 0.000
#&gt; SRR1927026     4  0.0000      0.989 0.000 0.000 0.000 1.000
#&gt; SRR1927024     4  0.0000      0.989 0.000 0.000 0.000 1.000
#&gt; SRR1927025     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR1927023     2  0.4830      0.355 0.000 0.608 0.392 0.000
#&gt; SRR1927022     4  0.2530      0.866 0.112 0.000 0.000 0.888
#&gt; SRR1927021     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR1927020     4  0.0000      0.989 0.000 0.000 0.000 1.000
#&gt; SRR1927019     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR1927071     4  0.0000      0.989 0.000 0.000 0.000 1.000
#&gt; SRR1927069     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR1927070     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927068     4  0.0000      0.989 0.000 0.000 0.000 1.000
#&gt; SRR1927066     4  0.0000      0.989 0.000 0.000 0.000 1.000
#&gt; SRR1927065     3  0.0000      0.999 0.000 0.000 1.000 0.000
#&gt; SRR1927067     3  0.0000      0.999 0.000 0.000 1.000 0.000
#&gt; SRR1927064     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927063     2  0.0000      0.975 0.000 1.000 0.000 0.000
#&gt; SRR1927062     4  0.0000      0.989 0.000 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-3-a').click(function(){
  $('#tab-SD-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-4'>
<p><a id='tab-SD-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1927048     1  0.0609      0.987 0.980 0.000 0.000 0.000 0.020
#&gt; SRR1927061     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927060     1  0.0000      0.990 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927058     1  0.0000      0.990 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927057     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927055     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927056     4  0.0609      0.974 0.000 0.000 0.000 0.980 0.020
#&gt; SRR1927054     1  0.0000      0.990 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927052     4  0.0290      0.975 0.000 0.000 0.000 0.992 0.008
#&gt; SRR1927053     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927051     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927050     4  0.0609      0.974 0.000 0.000 0.000 0.980 0.020
#&gt; SRR1927049     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927047     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927046     1  0.0703      0.986 0.976 0.000 0.000 0.000 0.024
#&gt; SRR1927045     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927044     1  0.0703      0.986 0.976 0.000 0.000 0.000 0.024
#&gt; SRR1927043     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927042     1  0.0000      0.990 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      0.990 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927039     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927038     1  0.0000      0.990 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927036     1  0.0703      0.986 0.976 0.000 0.000 0.000 0.024
#&gt; SRR1927035     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927034     4  0.0609      0.974 0.000 0.000 0.000 0.980 0.020
#&gt; SRR1927033     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927032     1  0.0000      0.990 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927031     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927030     1  0.0703      0.986 0.976 0.000 0.000 0.000 0.024
#&gt; SRR1927028     4  0.0000      0.976 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927029     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927027     5  0.1608      0.871 0.000 0.000 0.072 0.000 0.928
#&gt; SRR1927026     4  0.0000      0.976 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927024     4  0.0162      0.976 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1927025     5  0.1851      0.902 0.000 0.088 0.000 0.000 0.912
#&gt; SRR1927023     5  0.1197      0.923 0.000 0.048 0.000 0.000 0.952
#&gt; SRR1927022     4  0.2848      0.825 0.104 0.000 0.000 0.868 0.028
#&gt; SRR1927021     2  0.0963      0.962 0.000 0.964 0.000 0.000 0.036
#&gt; SRR1927020     4  0.0609      0.974 0.000 0.000 0.000 0.980 0.020
#&gt; SRR1927019     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927071     4  0.0162      0.976 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1927069     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927070     1  0.0703      0.986 0.976 0.000 0.000 0.000 0.024
#&gt; SRR1927068     4  0.0609      0.974 0.000 0.000 0.000 0.980 0.020
#&gt; SRR1927066     4  0.0290      0.975 0.000 0.000 0.000 0.992 0.008
#&gt; SRR1927065     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927067     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927064     1  0.0000      0.990 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927063     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927062     4  0.0290      0.975 0.000 0.000 0.000 0.992 0.008
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-4-a').click(function(){
  $('#tab-SD-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-5'>
<p><a id='tab-SD-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1927048     1  0.1327      0.911 0.936 0.000 0.000 0.000 0.064 0.000
#&gt; SRR1927061     3  0.0146      0.816 0.000 0.004 0.996 0.000 0.000 0.000
#&gt; SRR1927060     1  0.0000      0.922 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.1204      0.962 0.000 0.944 0.000 0.000 0.056 0.000
#&gt; SRR1927058     1  0.0000      0.922 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927057     2  0.1141      0.962 0.000 0.948 0.000 0.000 0.052 0.000
#&gt; SRR1927055     3  0.3862      0.289 0.000 0.000 0.524 0.000 0.000 0.476
#&gt; SRR1927056     4  0.2454      0.874 0.000 0.000 0.000 0.840 0.160 0.000
#&gt; SRR1927054     1  0.0000      0.922 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927052     4  0.0713      0.885 0.000 0.000 0.000 0.972 0.028 0.000
#&gt; SRR1927053     2  0.1204      0.962 0.000 0.944 0.000 0.000 0.056 0.000
#&gt; SRR1927051     2  0.0000      0.969 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927050     4  0.2454      0.874 0.000 0.000 0.000 0.840 0.160 0.000
#&gt; SRR1927049     2  0.0000      0.969 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927047     2  0.0363      0.969 0.000 0.988 0.000 0.000 0.012 0.000
#&gt; SRR1927046     1  0.2697      0.871 0.812 0.000 0.000 0.000 0.188 0.000
#&gt; SRR1927045     2  0.0363      0.963 0.000 0.988 0.012 0.000 0.000 0.000
#&gt; SRR1927044     1  0.2697      0.871 0.812 0.000 0.000 0.000 0.188 0.000
#&gt; SRR1927043     3  0.0000      0.820 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927042     1  0.0000      0.922 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      0.922 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927039     2  0.1204      0.962 0.000 0.944 0.000 0.000 0.056 0.000
#&gt; SRR1927038     1  0.0000      0.922 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.1141      0.962 0.000 0.948 0.000 0.000 0.052 0.000
#&gt; SRR1927036     1  0.2697      0.871 0.812 0.000 0.000 0.000 0.188 0.000
#&gt; SRR1927035     2  0.0000      0.969 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927034     4  0.2454      0.874 0.000 0.000 0.000 0.840 0.160 0.000
#&gt; SRR1927033     3  0.3860      0.297 0.000 0.000 0.528 0.000 0.000 0.472
#&gt; SRR1927032     1  0.0000      0.922 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927031     2  0.1204      0.962 0.000 0.944 0.000 0.000 0.056 0.000
#&gt; SRR1927030     1  0.2697      0.871 0.812 0.000 0.000 0.000 0.188 0.000
#&gt; SRR1927028     4  0.0713      0.894 0.000 0.000 0.000 0.972 0.028 0.000
#&gt; SRR1927029     3  0.0000      0.820 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927027     6  0.0405      0.000 0.000 0.000 0.008 0.000 0.004 0.988
#&gt; SRR1927026     4  0.1219      0.893 0.000 0.000 0.000 0.948 0.048 0.004
#&gt; SRR1927024     4  0.1010      0.879 0.000 0.000 0.000 0.960 0.036 0.004
#&gt; SRR1927025     5  0.4619      0.862 0.000 0.044 0.000 0.000 0.564 0.392
#&gt; SRR1927023     5  0.3828      0.857 0.000 0.000 0.000 0.000 0.560 0.440
#&gt; SRR1927022     4  0.4637      0.536 0.088 0.000 0.000 0.684 0.224 0.004
#&gt; SRR1927021     2  0.1908      0.884 0.000 0.900 0.000 0.000 0.096 0.004
#&gt; SRR1927020     4  0.2454      0.874 0.000 0.000 0.000 0.840 0.160 0.000
#&gt; SRR1927019     2  0.0000      0.969 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927071     4  0.0146      0.891 0.000 0.000 0.000 0.996 0.004 0.000
#&gt; SRR1927069     2  0.0146      0.968 0.000 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1927070     1  0.2697      0.871 0.812 0.000 0.000 0.000 0.188 0.000
#&gt; SRR1927068     4  0.2454      0.874 0.000 0.000 0.000 0.840 0.160 0.000
#&gt; SRR1927066     4  0.0547      0.888 0.000 0.000 0.000 0.980 0.020 0.000
#&gt; SRR1927065     3  0.0000      0.820 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927067     3  0.0000      0.820 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927064     1  0.0363      0.921 0.988 0.000 0.000 0.000 0.012 0.000
#&gt; SRR1927063     2  0.0000      0.969 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927062     4  0.0458      0.891 0.000 0.000 0.000 0.984 0.016 0.000
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-5-a').click(function(){
  $('#tab-SD-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-SD-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-signatures'>
<ul>
<li><a href='#tab-SD-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-skmeans-signature_compare](figure_cola/SD-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-SD-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-skmeans-collect-classes](figure_cola/SD-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:pam*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "pam"]
# you can also extract it by
# res = res_list["SD:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16868 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-pam-collect-plots](figure_cola/SD-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-pam-select-partition-number](figure_cola/SD-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5095 0.491   0.491
#> 3 3 0.914           0.938       0.967         0.2701 0.841   0.681
#> 4 4 0.911           0.936       0.965         0.1500 0.897   0.708
#> 5 5 0.901           0.863       0.906         0.0556 0.947   0.801
#> 6 6 0.908           0.889       0.913         0.0298 0.971   0.868
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2 3 4 5
```

There is also optional best $k$ = 2 3 4 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-classes'>
<ul>
<li><a href='#tab-SD-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-pam-get-classes-1'>
<p><a id='tab-SD-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1927048     1       0          1  1  0
#&gt; SRR1927061     2       0          1  0  1
#&gt; SRR1927060     1       0          1  1  0
#&gt; SRR1927059     2       0          1  0  1
#&gt; SRR1927058     1       0          1  1  0
#&gt; SRR1927057     2       0          1  0  1
#&gt; SRR1927055     2       0          1  0  1
#&gt; SRR1927056     1       0          1  1  0
#&gt; SRR1927054     1       0          1  1  0
#&gt; SRR1927052     1       0          1  1  0
#&gt; SRR1927053     2       0          1  0  1
#&gt; SRR1927051     2       0          1  0  1
#&gt; SRR1927050     1       0          1  1  0
#&gt; SRR1927049     2       0          1  0  1
#&gt; SRR1927047     2       0          1  0  1
#&gt; SRR1927046     1       0          1  1  0
#&gt; SRR1927045     2       0          1  0  1
#&gt; SRR1927044     1       0          1  1  0
#&gt; SRR1927043     2       0          1  0  1
#&gt; SRR1927042     1       0          1  1  0
#&gt; SRR1927040     1       0          1  1  0
#&gt; SRR1927039     2       0          1  0  1
#&gt; SRR1927038     1       0          1  1  0
#&gt; SRR1927037     2       0          1  0  1
#&gt; SRR1927036     1       0          1  1  0
#&gt; SRR1927035     2       0          1  0  1
#&gt; SRR1927034     1       0          1  1  0
#&gt; SRR1927033     2       0          1  0  1
#&gt; SRR1927032     1       0          1  1  0
#&gt; SRR1927031     2       0          1  0  1
#&gt; SRR1927030     1       0          1  1  0
#&gt; SRR1927028     1       0          1  1  0
#&gt; SRR1927029     2       0          1  0  1
#&gt; SRR1927027     2       0          1  0  1
#&gt; SRR1927026     1       0          1  1  0
#&gt; SRR1927024     1       0          1  1  0
#&gt; SRR1927025     2       0          1  0  1
#&gt; SRR1927023     2       0          1  0  1
#&gt; SRR1927022     1       0          1  1  0
#&gt; SRR1927021     2       0          1  0  1
#&gt; SRR1927020     1       0          1  1  0
#&gt; SRR1927019     2       0          1  0  1
#&gt; SRR1927071     1       0          1  1  0
#&gt; SRR1927069     2       0          1  0  1
#&gt; SRR1927070     1       0          1  1  0
#&gt; SRR1927068     1       0          1  1  0
#&gt; SRR1927066     1       0          1  1  0
#&gt; SRR1927065     2       0          1  0  1
#&gt; SRR1927067     2       0          1  0  1
#&gt; SRR1927064     1       0          1  1  0
#&gt; SRR1927063     2       0          1  0  1
#&gt; SRR1927062     1       0          1  1  0
</code></pre>

<script>
$('#tab-SD-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-1-a').click(function(){
  $('#tab-SD-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-2'>
<p><a id='tab-SD-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1927048     1  0.0000      0.918 1.000 0.000 0.000
#&gt; SRR1927061     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927060     1  0.0000      0.918 1.000 0.000 0.000
#&gt; SRR1927059     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927058     1  0.0000      0.918 1.000 0.000 0.000
#&gt; SRR1927057     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927055     2  0.2165      0.928 0.000 0.936 0.064
#&gt; SRR1927056     3  0.0000      0.945 0.000 0.000 1.000
#&gt; SRR1927054     1  0.0000      0.918 1.000 0.000 0.000
#&gt; SRR1927052     1  0.5016      0.786 0.760 0.000 0.240
#&gt; SRR1927053     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927051     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927050     3  0.0000      0.945 0.000 0.000 1.000
#&gt; SRR1927049     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927047     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927046     1  0.2356      0.902 0.928 0.000 0.072
#&gt; SRR1927045     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927044     1  0.4178      0.863 0.828 0.000 0.172
#&gt; SRR1927043     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927042     1  0.0000      0.918 1.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      0.918 1.000 0.000 0.000
#&gt; SRR1927039     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927038     1  0.0000      0.918 1.000 0.000 0.000
#&gt; SRR1927037     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927036     1  0.4178      0.863 0.828 0.000 0.172
#&gt; SRR1927035     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927034     3  0.0000      0.945 0.000 0.000 1.000
#&gt; SRR1927033     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927032     1  0.0000      0.918 1.000 0.000 0.000
#&gt; SRR1927031     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927030     1  0.4121      0.865 0.832 0.000 0.168
#&gt; SRR1927028     3  0.0000      0.945 0.000 0.000 1.000
#&gt; SRR1927029     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927027     3  0.6126      0.320 0.000 0.400 0.600
#&gt; SRR1927026     3  0.0000      0.945 0.000 0.000 1.000
#&gt; SRR1927024     3  0.0892      0.929 0.020 0.000 0.980
#&gt; SRR1927025     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927023     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927022     1  0.4178      0.863 0.828 0.000 0.172
#&gt; SRR1927021     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927020     3  0.0000      0.945 0.000 0.000 1.000
#&gt; SRR1927019     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927071     3  0.0000      0.945 0.000 0.000 1.000
#&gt; SRR1927069     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927070     1  0.4178      0.863 0.828 0.000 0.172
#&gt; SRR1927068     3  0.0000      0.945 0.000 0.000 1.000
#&gt; SRR1927066     3  0.1860      0.897 0.052 0.000 0.948
#&gt; SRR1927065     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927067     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927064     1  0.0000      0.918 1.000 0.000 0.000
#&gt; SRR1927063     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1927062     3  0.0000      0.945 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-2-a').click(function(){
  $('#tab-SD-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-3'>
<p><a id='tab-SD-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1927048     1  0.0000      0.915 1.000 0.000 0.000 0.000
#&gt; SRR1927061     3  0.0000      0.958 0.000 0.000 1.000 0.000
#&gt; SRR1927060     1  0.0000      0.915 1.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.0000      0.982 0.000 1.000 0.000 0.000
#&gt; SRR1927058     1  0.0000      0.915 1.000 0.000 0.000 0.000
#&gt; SRR1927057     2  0.0000      0.982 0.000 1.000 0.000 0.000
#&gt; SRR1927055     3  0.0000      0.958 0.000 0.000 1.000 0.000
#&gt; SRR1927056     4  0.0000      0.991 0.000 0.000 0.000 1.000
#&gt; SRR1927054     1  0.0000      0.915 1.000 0.000 0.000 0.000
#&gt; SRR1927052     1  0.4008      0.777 0.756 0.000 0.000 0.244
#&gt; SRR1927053     2  0.0000      0.982 0.000 1.000 0.000 0.000
#&gt; SRR1927051     2  0.0000      0.982 0.000 1.000 0.000 0.000
#&gt; SRR1927050     4  0.0000      0.991 0.000 0.000 0.000 1.000
#&gt; SRR1927049     2  0.0000      0.982 0.000 1.000 0.000 0.000
#&gt; SRR1927047     2  0.0000      0.982 0.000 1.000 0.000 0.000
#&gt; SRR1927046     1  0.1867      0.901 0.928 0.000 0.000 0.072
#&gt; SRR1927045     2  0.0000      0.982 0.000 1.000 0.000 0.000
#&gt; SRR1927044     1  0.3311      0.861 0.828 0.000 0.000 0.172
#&gt; SRR1927043     3  0.0000      0.958 0.000 0.000 1.000 0.000
#&gt; SRR1927042     1  0.0000      0.915 1.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      0.915 1.000 0.000 0.000 0.000
#&gt; SRR1927039     2  0.0000      0.982 0.000 1.000 0.000 0.000
#&gt; SRR1927038     1  0.0000      0.915 1.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.0000      0.982 0.000 1.000 0.000 0.000
#&gt; SRR1927036     1  0.3311      0.861 0.828 0.000 0.000 0.172
#&gt; SRR1927035     2  0.0000      0.982 0.000 1.000 0.000 0.000
#&gt; SRR1927034     4  0.0000      0.991 0.000 0.000 0.000 1.000
#&gt; SRR1927033     3  0.0000      0.958 0.000 0.000 1.000 0.000
#&gt; SRR1927032     1  0.0000      0.915 1.000 0.000 0.000 0.000
#&gt; SRR1927031     2  0.0000      0.982 0.000 1.000 0.000 0.000
#&gt; SRR1927030     1  0.3266      0.863 0.832 0.000 0.000 0.168
#&gt; SRR1927028     4  0.0000      0.991 0.000 0.000 0.000 1.000
#&gt; SRR1927029     3  0.0000      0.958 0.000 0.000 1.000 0.000
#&gt; SRR1927027     3  0.4304      0.598 0.000 0.000 0.716 0.284
#&gt; SRR1927026     4  0.0000      0.991 0.000 0.000 0.000 1.000
#&gt; SRR1927024     4  0.0707      0.973 0.020 0.000 0.000 0.980
#&gt; SRR1927025     2  0.0469      0.972 0.000 0.988 0.012 0.000
#&gt; SRR1927023     2  0.4222      0.634 0.000 0.728 0.272 0.000
#&gt; SRR1927022     1  0.3356      0.857 0.824 0.000 0.000 0.176
#&gt; SRR1927021     2  0.0000      0.982 0.000 1.000 0.000 0.000
#&gt; SRR1927020     4  0.0000      0.991 0.000 0.000 0.000 1.000
#&gt; SRR1927019     2  0.0000      0.982 0.000 1.000 0.000 0.000
#&gt; SRR1927071     4  0.0000      0.991 0.000 0.000 0.000 1.000
#&gt; SRR1927069     2  0.0000      0.982 0.000 1.000 0.000 0.000
#&gt; SRR1927070     1  0.3311      0.861 0.828 0.000 0.000 0.172
#&gt; SRR1927068     4  0.0000      0.991 0.000 0.000 0.000 1.000
#&gt; SRR1927066     4  0.1474      0.937 0.052 0.000 0.000 0.948
#&gt; SRR1927065     3  0.0000      0.958 0.000 0.000 1.000 0.000
#&gt; SRR1927067     3  0.0000      0.958 0.000 0.000 1.000 0.000
#&gt; SRR1927064     1  0.0000      0.915 1.000 0.000 0.000 0.000
#&gt; SRR1927063     2  0.0000      0.982 0.000 1.000 0.000 0.000
#&gt; SRR1927062     4  0.0000      0.991 0.000 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-3-a').click(function(){
  $('#tab-SD-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-4'>
<p><a id='tab-SD-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1927048     1  0.0290      0.821 0.992 0.000 0.000 0.000 0.008
#&gt; SRR1927061     3  0.0000      0.934 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927060     1  0.3774      0.789 0.704 0.000 0.000 0.000 0.296
#&gt; SRR1927059     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927058     1  0.3774      0.789 0.704 0.000 0.000 0.000 0.296
#&gt; SRR1927057     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927055     3  0.0000      0.934 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927056     5  0.3774      1.000 0.000 0.000 0.000 0.296 0.704
#&gt; SRR1927054     1  0.3774      0.789 0.704 0.000 0.000 0.000 0.296
#&gt; SRR1927052     4  0.3774      0.711 0.296 0.000 0.000 0.704 0.000
#&gt; SRR1927053     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927051     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927050     5  0.3774      1.000 0.000 0.000 0.000 0.296 0.704
#&gt; SRR1927049     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927047     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927046     1  0.0000      0.819 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927045     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927044     1  0.1851      0.767 0.912 0.000 0.000 0.088 0.000
#&gt; SRR1927043     3  0.0000      0.934 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927042     1  0.0000      0.819 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.3774      0.789 0.704 0.000 0.000 0.000 0.296
#&gt; SRR1927039     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927038     1  0.3774      0.789 0.704 0.000 0.000 0.000 0.296
#&gt; SRR1927037     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927036     1  0.1851      0.767 0.912 0.000 0.000 0.088 0.000
#&gt; SRR1927035     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927034     5  0.3774      1.000 0.000 0.000 0.000 0.296 0.704
#&gt; SRR1927033     3  0.0000      0.934 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927032     1  0.3424      0.802 0.760 0.000 0.000 0.000 0.240
#&gt; SRR1927031     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927030     1  0.1197      0.796 0.952 0.000 0.000 0.048 0.000
#&gt; SRR1927028     4  0.0000      0.730 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927029     3  0.0000      0.934 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927027     3  0.4273      0.220 0.000 0.000 0.552 0.000 0.448
#&gt; SRR1927026     4  0.1908      0.591 0.000 0.000 0.000 0.908 0.092
#&gt; SRR1927024     4  0.2020      0.750 0.100 0.000 0.000 0.900 0.000
#&gt; SRR1927025     2  0.0404      0.971 0.000 0.988 0.012 0.000 0.000
#&gt; SRR1927023     2  0.3636      0.631 0.000 0.728 0.272 0.000 0.000
#&gt; SRR1927022     4  0.3774      0.711 0.296 0.000 0.000 0.704 0.000
#&gt; SRR1927021     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927020     5  0.3774      1.000 0.000 0.000 0.000 0.296 0.704
#&gt; SRR1927019     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927071     4  0.0000      0.730 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927069     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927070     1  0.1851      0.767 0.912 0.000 0.000 0.088 0.000
#&gt; SRR1927068     5  0.3774      1.000 0.000 0.000 0.000 0.296 0.704
#&gt; SRR1927066     4  0.3774      0.711 0.296 0.000 0.000 0.704 0.000
#&gt; SRR1927065     3  0.0000      0.934 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927067     3  0.0000      0.934 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927064     1  0.1043      0.823 0.960 0.000 0.000 0.000 0.040
#&gt; SRR1927063     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927062     4  0.0162      0.727 0.000 0.000 0.000 0.996 0.004
</code></pre>

<script>
$('#tab-SD-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-4-a').click(function(){
  $('#tab-SD-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-5'>
<p><a id='tab-SD-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1927048     1  0.3351      0.821 0.712 0.000 0.000 0.288 0.000 0.000
#&gt; SRR1927061     3  0.0000      0.998 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927060     1  0.0000      0.774 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927058     1  0.0000      0.774 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927057     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927055     3  0.0260      0.994 0.000 0.000 0.992 0.000 0.008 0.000
#&gt; SRR1927056     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1927054     1  0.0000      0.774 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927052     4  0.0000      0.698 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927053     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927051     2  0.0363      0.993 0.000 0.988 0.000 0.000 0.012 0.000
#&gt; SRR1927050     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1927049     2  0.0363      0.993 0.000 0.988 0.000 0.000 0.012 0.000
#&gt; SRR1927047     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927046     1  0.3390      0.819 0.704 0.000 0.000 0.296 0.000 0.000
#&gt; SRR1927045     2  0.0725      0.983 0.000 0.976 0.012 0.000 0.012 0.000
#&gt; SRR1927044     1  0.3717      0.767 0.616 0.000 0.000 0.384 0.000 0.000
#&gt; SRR1927043     3  0.0000      0.998 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927042     1  0.3390      0.819 0.704 0.000 0.000 0.296 0.000 0.000
#&gt; SRR1927040     1  0.0000      0.774 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927039     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927038     1  0.0000      0.774 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927036     1  0.3717      0.767 0.616 0.000 0.000 0.384 0.000 0.000
#&gt; SRR1927035     2  0.0363      0.993 0.000 0.988 0.000 0.000 0.012 0.000
#&gt; SRR1927034     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1927033     3  0.0260      0.994 0.000 0.000 0.992 0.000 0.008 0.000
#&gt; SRR1927032     1  0.1204      0.790 0.944 0.000 0.000 0.056 0.000 0.000
#&gt; SRR1927031     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927030     1  0.3592      0.796 0.656 0.000 0.000 0.344 0.000 0.000
#&gt; SRR1927028     4  0.3390      0.726 0.000 0.000 0.000 0.704 0.000 0.296
#&gt; SRR1927029     3  0.0000      0.998 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927027     5  0.0993      0.920 0.000 0.000 0.012 0.000 0.964 0.024
#&gt; SRR1927026     4  0.3727      0.583 0.000 0.000 0.000 0.612 0.000 0.388
#&gt; SRR1927024     4  0.2762      0.746 0.000 0.000 0.000 0.804 0.000 0.196
#&gt; SRR1927025     5  0.1387      0.898 0.000 0.068 0.000 0.000 0.932 0.000
#&gt; SRR1927023     5  0.0260      0.935 0.000 0.008 0.000 0.000 0.992 0.000
#&gt; SRR1927022     4  0.0000      0.698 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927021     2  0.0363      0.993 0.000 0.988 0.000 0.000 0.012 0.000
#&gt; SRR1927020     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1927019     2  0.0363      0.993 0.000 0.988 0.000 0.000 0.012 0.000
#&gt; SRR1927071     4  0.3390      0.726 0.000 0.000 0.000 0.704 0.000 0.296
#&gt; SRR1927069     2  0.0363      0.993 0.000 0.988 0.000 0.000 0.012 0.000
#&gt; SRR1927070     1  0.3717      0.767 0.616 0.000 0.000 0.384 0.000 0.000
#&gt; SRR1927068     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1927066     4  0.0000      0.698 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927065     3  0.0000      0.998 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927067     3  0.0000      0.998 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927064     1  0.3175      0.823 0.744 0.000 0.000 0.256 0.000 0.000
#&gt; SRR1927063     2  0.0363      0.993 0.000 0.988 0.000 0.000 0.012 0.000
#&gt; SRR1927062     4  0.3409      0.723 0.000 0.000 0.000 0.700 0.000 0.300
</code></pre>

<script>
$('#tab-SD-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-5-a').click(function(){
  $('#tab-SD-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-pam-membership-heatmap'>
<ul>
<li><a href='#tab-SD-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-signatures'>
<ul>
<li><a href='#tab-SD-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-1-1.png" alt="plot of chunk tab-SD-pam-get-signatures-1"/></p>

</div>
<div id='tab-SD-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-2-1.png" alt="plot of chunk tab-SD-pam-get-signatures-2"/></p>

</div>
<div id='tab-SD-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-3-1.png" alt="plot of chunk tab-SD-pam-get-signatures-3"/></p>

</div>
<div id='tab-SD-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-4-1.png" alt="plot of chunk tab-SD-pam-get-signatures-4"/></p>

</div>
<div id='tab-SD-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-5-1.png" alt="plot of chunk tab-SD-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-pam-signature_compare](figure_cola/SD-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-pam-dimension-reduction'>
<ul>
<li><a href='#tab-SD-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-pam-collect-classes](figure_cola/SD-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:mclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "mclust"]
# you can also extract it by
# res = res_list["SD:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16868 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 5.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-mclust-collect-plots](figure_cola/SD-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-mclust-select-partition-number](figure_cola/SD-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5095 0.491   0.491
#> 3 3 1.000           0.974       0.979         0.0841 0.965   0.929
#> 4 4 0.738           0.826       0.872         0.3024 0.777   0.520
#> 5 5 0.958           0.883       0.945         0.0718 0.959   0.843
#> 6 6 0.877           0.793       0.898         0.0383 0.922   0.687
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 5
#> attr(,"optional")
#> [1] 2 3
```

There is also optional best $k$ = 2 3 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-classes'>
<ul>
<li><a href='#tab-SD-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-mclust-get-classes-1'>
<p><a id='tab-SD-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1927048     1       0          1  1  0
#&gt; SRR1927061     2       0          1  0  1
#&gt; SRR1927060     1       0          1  1  0
#&gt; SRR1927059     2       0          1  0  1
#&gt; SRR1927058     1       0          1  1  0
#&gt; SRR1927057     2       0          1  0  1
#&gt; SRR1927055     2       0          1  0  1
#&gt; SRR1927056     1       0          1  1  0
#&gt; SRR1927054     1       0          1  1  0
#&gt; SRR1927052     1       0          1  1  0
#&gt; SRR1927053     2       0          1  0  1
#&gt; SRR1927051     2       0          1  0  1
#&gt; SRR1927050     1       0          1  1  0
#&gt; SRR1927049     2       0          1  0  1
#&gt; SRR1927047     2       0          1  0  1
#&gt; SRR1927046     1       0          1  1  0
#&gt; SRR1927045     2       0          1  0  1
#&gt; SRR1927044     1       0          1  1  0
#&gt; SRR1927043     2       0          1  0  1
#&gt; SRR1927042     1       0          1  1  0
#&gt; SRR1927040     1       0          1  1  0
#&gt; SRR1927039     2       0          1  0  1
#&gt; SRR1927038     1       0          1  1  0
#&gt; SRR1927037     2       0          1  0  1
#&gt; SRR1927036     1       0          1  1  0
#&gt; SRR1927035     2       0          1  0  1
#&gt; SRR1927034     1       0          1  1  0
#&gt; SRR1927033     2       0          1  0  1
#&gt; SRR1927032     1       0          1  1  0
#&gt; SRR1927031     2       0          1  0  1
#&gt; SRR1927030     1       0          1  1  0
#&gt; SRR1927028     1       0          1  1  0
#&gt; SRR1927029     2       0          1  0  1
#&gt; SRR1927027     2       0          1  0  1
#&gt; SRR1927026     1       0          1  1  0
#&gt; SRR1927024     1       0          1  1  0
#&gt; SRR1927025     2       0          1  0  1
#&gt; SRR1927023     2       0          1  0  1
#&gt; SRR1927022     1       0          1  1  0
#&gt; SRR1927021     2       0          1  0  1
#&gt; SRR1927020     1       0          1  1  0
#&gt; SRR1927019     2       0          1  0  1
#&gt; SRR1927071     1       0          1  1  0
#&gt; SRR1927069     2       0          1  0  1
#&gt; SRR1927070     1       0          1  1  0
#&gt; SRR1927068     1       0          1  1  0
#&gt; SRR1927066     1       0          1  1  0
#&gt; SRR1927065     2       0          1  0  1
#&gt; SRR1927067     2       0          1  0  1
#&gt; SRR1927064     1       0          1  1  0
#&gt; SRR1927063     2       0          1  0  1
#&gt; SRR1927062     1       0          1  1  0
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-1-a').click(function(){
  $('#tab-SD-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-2'>
<p><a id='tab-SD-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1    p2    p3
#&gt; SRR1927048     1  0.0000      1.000  1 0.000 0.000
#&gt; SRR1927061     2  0.0000      0.955  0 1.000 0.000
#&gt; SRR1927060     1  0.0000      1.000  1 0.000 0.000
#&gt; SRR1927059     2  0.2711      0.935  0 0.912 0.088
#&gt; SRR1927058     1  0.0000      1.000  1 0.000 0.000
#&gt; SRR1927057     2  0.2711      0.935  0 0.912 0.088
#&gt; SRR1927055     2  0.0237      0.953  0 0.996 0.004
#&gt; SRR1927056     1  0.0000      1.000  1 0.000 0.000
#&gt; SRR1927054     1  0.0000      1.000  1 0.000 0.000
#&gt; SRR1927052     1  0.0000      1.000  1 0.000 0.000
#&gt; SRR1927053     2  0.2711      0.935  0 0.912 0.088
#&gt; SRR1927051     2  0.0000      0.955  0 1.000 0.000
#&gt; SRR1927050     1  0.0000      1.000  1 0.000 0.000
#&gt; SRR1927049     2  0.0000      0.955  0 1.000 0.000
#&gt; SRR1927047     2  0.2711      0.935  0 0.912 0.088
#&gt; SRR1927046     1  0.0000      1.000  1 0.000 0.000
#&gt; SRR1927045     2  0.0000      0.955  0 1.000 0.000
#&gt; SRR1927044     1  0.0000      1.000  1 0.000 0.000
#&gt; SRR1927043     2  0.0000      0.955  0 1.000 0.000
#&gt; SRR1927042     1  0.0000      1.000  1 0.000 0.000
#&gt; SRR1927040     1  0.0000      1.000  1 0.000 0.000
#&gt; SRR1927039     2  0.2711      0.935  0 0.912 0.088
#&gt; SRR1927038     1  0.0000      1.000  1 0.000 0.000
#&gt; SRR1927037     2  0.2711      0.935  0 0.912 0.088
#&gt; SRR1927036     1  0.0000      1.000  1 0.000 0.000
#&gt; SRR1927035     2  0.2711      0.935  0 0.912 0.088
#&gt; SRR1927034     1  0.0000      1.000  1 0.000 0.000
#&gt; SRR1927033     2  0.3192      0.848  0 0.888 0.112
#&gt; SRR1927032     1  0.0000      1.000  1 0.000 0.000
#&gt; SRR1927031     2  0.2711      0.935  0 0.912 0.088
#&gt; SRR1927030     1  0.0000      1.000  1 0.000 0.000
#&gt; SRR1927028     1  0.0000      1.000  1 0.000 0.000
#&gt; SRR1927029     2  0.0000      0.955  0 1.000 0.000
#&gt; SRR1927027     3  0.2711      1.000  0 0.088 0.912
#&gt; SRR1927026     1  0.0000      1.000  1 0.000 0.000
#&gt; SRR1927024     1  0.0000      1.000  1 0.000 0.000
#&gt; SRR1927025     2  0.0237      0.953  0 0.996 0.004
#&gt; SRR1927023     3  0.2711      1.000  0 0.088 0.912
#&gt; SRR1927022     1  0.0000      1.000  1 0.000 0.000
#&gt; SRR1927021     2  0.0237      0.953  0 0.996 0.004
#&gt; SRR1927020     1  0.0000      1.000  1 0.000 0.000
#&gt; SRR1927019     2  0.0000      0.955  0 1.000 0.000
#&gt; SRR1927071     1  0.0000      1.000  1 0.000 0.000
#&gt; SRR1927069     2  0.2537      0.937  0 0.920 0.080
#&gt; SRR1927070     1  0.0000      1.000  1 0.000 0.000
#&gt; SRR1927068     1  0.0000      1.000  1 0.000 0.000
#&gt; SRR1927066     1  0.0000      1.000  1 0.000 0.000
#&gt; SRR1927065     2  0.0000      0.955  0 1.000 0.000
#&gt; SRR1927067     2  0.0000      0.955  0 1.000 0.000
#&gt; SRR1927064     1  0.0000      1.000  1 0.000 0.000
#&gt; SRR1927063     2  0.0000      0.955  0 1.000 0.000
#&gt; SRR1927062     1  0.0000      1.000  1 0.000 0.000
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-2-a').click(function(){
  $('#tab-SD-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-3'>
<p><a id='tab-SD-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1927048     1  0.3444     1.0000 0.816 0.000 0.000 0.184
#&gt; SRR1927061     2  0.5289     0.4567 0.020 0.636 0.344 0.000
#&gt; SRR1927060     1  0.3444     1.0000 0.816 0.000 0.000 0.184
#&gt; SRR1927059     2  0.0000     0.8572 0.000 1.000 0.000 0.000
#&gt; SRR1927058     1  0.3444     1.0000 0.816 0.000 0.000 0.184
#&gt; SRR1927057     2  0.0817     0.8480 0.000 0.976 0.024 0.000
#&gt; SRR1927055     3  0.0000     0.6379 0.000 0.000 1.000 0.000
#&gt; SRR1927056     4  0.0000     0.9877 0.000 0.000 0.000 1.000
#&gt; SRR1927054     1  0.3444     1.0000 0.816 0.000 0.000 0.184
#&gt; SRR1927052     4  0.0707     0.9770 0.020 0.000 0.000 0.980
#&gt; SRR1927053     2  0.0000     0.8572 0.000 1.000 0.000 0.000
#&gt; SRR1927051     2  0.3647     0.7939 0.016 0.832 0.152 0.000
#&gt; SRR1927050     4  0.0000     0.9877 0.000 0.000 0.000 1.000
#&gt; SRR1927049     2  0.3695     0.7917 0.016 0.828 0.156 0.000
#&gt; SRR1927047     2  0.0000     0.8572 0.000 1.000 0.000 0.000
#&gt; SRR1927046     1  0.3444     1.0000 0.816 0.000 0.000 0.184
#&gt; SRR1927045     2  0.3647     0.7948 0.016 0.832 0.152 0.000
#&gt; SRR1927044     1  0.3444     1.0000 0.816 0.000 0.000 0.184
#&gt; SRR1927043     3  0.5294    -0.0330 0.008 0.484 0.508 0.000
#&gt; SRR1927042     1  0.3444     1.0000 0.816 0.000 0.000 0.184
#&gt; SRR1927040     1  0.3444     1.0000 0.816 0.000 0.000 0.184
#&gt; SRR1927039     2  0.0000     0.8572 0.000 1.000 0.000 0.000
#&gt; SRR1927038     1  0.3444     1.0000 0.816 0.000 0.000 0.184
#&gt; SRR1927037     2  0.0336     0.8548 0.000 0.992 0.008 0.000
#&gt; SRR1927036     1  0.3444     1.0000 0.816 0.000 0.000 0.184
#&gt; SRR1927035     2  0.0000     0.8572 0.000 1.000 0.000 0.000
#&gt; SRR1927034     4  0.0188     0.9843 0.004 0.000 0.000 0.996
#&gt; SRR1927033     3  0.2843     0.6508 0.088 0.020 0.892 0.000
#&gt; SRR1927032     1  0.3444     1.0000 0.816 0.000 0.000 0.184
#&gt; SRR1927031     2  0.0000     0.8572 0.000 1.000 0.000 0.000
#&gt; SRR1927030     1  0.3444     1.0000 0.816 0.000 0.000 0.184
#&gt; SRR1927028     4  0.0000     0.9877 0.000 0.000 0.000 1.000
#&gt; SRR1927029     3  0.5281     0.0451 0.008 0.464 0.528 0.000
#&gt; SRR1927027     3  0.3123     0.6387 0.156 0.000 0.844 0.000
#&gt; SRR1927026     4  0.0000     0.9877 0.000 0.000 0.000 1.000
#&gt; SRR1927024     4  0.0921     0.9690 0.028 0.000 0.000 0.972
#&gt; SRR1927025     3  0.4436     0.5834 0.020 0.216 0.764 0.000
#&gt; SRR1927023     3  0.4753     0.6333 0.128 0.084 0.788 0.000
#&gt; SRR1927022     4  0.1389     0.9474 0.048 0.000 0.000 0.952
#&gt; SRR1927021     2  0.1059     0.8489 0.016 0.972 0.012 0.000
#&gt; SRR1927020     4  0.0000     0.9877 0.000 0.000 0.000 1.000
#&gt; SRR1927019     2  0.3695     0.7917 0.016 0.828 0.156 0.000
#&gt; SRR1927071     4  0.0000     0.9877 0.000 0.000 0.000 1.000
#&gt; SRR1927069     2  0.0000     0.8572 0.000 1.000 0.000 0.000
#&gt; SRR1927070     1  0.3444     1.0000 0.816 0.000 0.000 0.184
#&gt; SRR1927068     4  0.0000     0.9877 0.000 0.000 0.000 1.000
#&gt; SRR1927066     4  0.0188     0.9861 0.004 0.000 0.000 0.996
#&gt; SRR1927065     2  0.5288     0.0161 0.008 0.520 0.472 0.000
#&gt; SRR1927067     3  0.5281     0.0451 0.008 0.464 0.528 0.000
#&gt; SRR1927064     1  0.3444     1.0000 0.816 0.000 0.000 0.184
#&gt; SRR1927063     2  0.3695     0.7917 0.016 0.828 0.156 0.000
#&gt; SRR1927062     4  0.0707     0.9761 0.020 0.000 0.000 0.980
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-3-a').click(function(){
  $('#tab-SD-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-4'>
<p><a id='tab-SD-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1927048     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927061     3  0.6793      0.364 0.000 0.332 0.376 0.000 0.292
#&gt; SRR1927060     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927058     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927057     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927055     3  0.0000      0.320 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927056     4  0.0404      0.973 0.012 0.000 0.000 0.988 0.000
#&gt; SRR1927054     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927052     4  0.0794      0.963 0.028 0.000 0.000 0.972 0.000
#&gt; SRR1927053     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927051     2  0.0912      0.973 0.000 0.972 0.016 0.000 0.012
#&gt; SRR1927050     4  0.0404      0.973 0.012 0.000 0.000 0.988 0.000
#&gt; SRR1927049     2  0.1018      0.971 0.000 0.968 0.016 0.000 0.016
#&gt; SRR1927047     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927046     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927045     2  0.0798      0.975 0.000 0.976 0.008 0.000 0.016
#&gt; SRR1927044     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927043     3  0.4392      0.638 0.000 0.008 0.612 0.000 0.380
#&gt; SRR1927042     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927039     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927038     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927036     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927035     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927034     4  0.0404      0.973 0.012 0.000 0.000 0.988 0.000
#&gt; SRR1927033     3  0.0807      0.286 0.000 0.000 0.976 0.012 0.012
#&gt; SRR1927032     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927031     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927030     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927028     4  0.0404      0.973 0.012 0.000 0.000 0.988 0.000
#&gt; SRR1927029     3  0.4276      0.638 0.000 0.004 0.616 0.000 0.380
#&gt; SRR1927027     5  0.4505      0.980 0.000 0.000 0.384 0.012 0.604
#&gt; SRR1927026     4  0.0404      0.973 0.012 0.000 0.000 0.988 0.000
#&gt; SRR1927024     4  0.0794      0.963 0.028 0.000 0.000 0.972 0.000
#&gt; SRR1927025     3  0.6708     -0.558 0.000 0.244 0.384 0.000 0.372
#&gt; SRR1927023     5  0.4126      0.980 0.000 0.000 0.380 0.000 0.620
#&gt; SRR1927022     4  0.2605      0.820 0.148 0.000 0.000 0.852 0.000
#&gt; SRR1927021     2  0.2189      0.906 0.000 0.904 0.012 0.000 0.084
#&gt; SRR1927020     4  0.0404      0.973 0.012 0.000 0.000 0.988 0.000
#&gt; SRR1927019     2  0.0912      0.973 0.000 0.972 0.016 0.000 0.012
#&gt; SRR1927071     4  0.0404      0.973 0.012 0.000 0.000 0.988 0.000
#&gt; SRR1927069     2  0.0000      0.982 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927070     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927068     4  0.0404      0.973 0.012 0.000 0.000 0.988 0.000
#&gt; SRR1927066     4  0.0404      0.973 0.012 0.000 0.000 0.988 0.000
#&gt; SRR1927065     3  0.4757      0.633 0.000 0.024 0.596 0.000 0.380
#&gt; SRR1927067     3  0.4276      0.638 0.000 0.004 0.616 0.000 0.380
#&gt; SRR1927064     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927063     2  0.1549      0.956 0.000 0.944 0.016 0.000 0.040
#&gt; SRR1927062     4  0.1965      0.888 0.096 0.000 0.000 0.904 0.000
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-4-a').click(function(){
  $('#tab-SD-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-5'>
<p><a id='tab-SD-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1927048     1  0.0146      0.969 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; SRR1927061     6  0.4769      0.701 0.000 0.164 0.160 0.000 0.000 0.676
#&gt; SRR1927060     1  0.0363      0.966 0.988 0.000 0.000 0.000 0.000 0.012
#&gt; SRR1927059     2  0.0000      0.737 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927058     1  0.0000      0.970 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927057     2  0.3966     -0.278 0.000 0.552 0.004 0.000 0.000 0.444
#&gt; SRR1927055     3  0.2340      0.796 0.000 0.000 0.852 0.000 0.148 0.000
#&gt; SRR1927056     4  0.0405      0.942 0.008 0.000 0.000 0.988 0.000 0.004
#&gt; SRR1927054     1  0.0000      0.970 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927052     4  0.0865      0.924 0.036 0.000 0.000 0.964 0.000 0.000
#&gt; SRR1927053     2  0.0000      0.737 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927051     6  0.3547      0.781 0.000 0.300 0.004 0.000 0.000 0.696
#&gt; SRR1927050     4  0.0458      0.937 0.000 0.000 0.000 0.984 0.000 0.016
#&gt; SRR1927049     6  0.3023      0.847 0.000 0.212 0.004 0.000 0.000 0.784
#&gt; SRR1927047     2  0.0000      0.737 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927046     1  0.0291      0.967 0.992 0.000 0.000 0.004 0.000 0.004
#&gt; SRR1927045     6  0.3804      0.525 0.000 0.424 0.000 0.000 0.000 0.576
#&gt; SRR1927044     1  0.0603      0.958 0.980 0.000 0.000 0.016 0.000 0.004
#&gt; SRR1927043     3  0.1088      0.900 0.000 0.016 0.960 0.000 0.000 0.024
#&gt; SRR1927042     1  0.0000      0.970 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0363      0.966 0.988 0.000 0.000 0.000 0.000 0.012
#&gt; SRR1927039     2  0.0000      0.737 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927038     1  0.0363      0.966 0.988 0.000 0.000 0.000 0.000 0.012
#&gt; SRR1927037     2  0.3833     -0.270 0.000 0.556 0.000 0.000 0.000 0.444
#&gt; SRR1927036     1  0.0146      0.969 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; SRR1927035     2  0.3747     -0.110 0.000 0.604 0.000 0.000 0.000 0.396
#&gt; SRR1927034     4  0.0713      0.931 0.000 0.000 0.000 0.972 0.000 0.028
#&gt; SRR1927033     3  0.2883      0.739 0.000 0.000 0.788 0.000 0.212 0.000
#&gt; SRR1927032     1  0.0000      0.970 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927031     2  0.0000      0.737 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927030     1  0.1010      0.938 0.960 0.000 0.000 0.036 0.000 0.004
#&gt; SRR1927028     4  0.0146      0.942 0.004 0.000 0.000 0.996 0.000 0.000
#&gt; SRR1927029     3  0.1088      0.900 0.000 0.016 0.960 0.000 0.000 0.024
#&gt; SRR1927027     5  0.0632      0.833 0.000 0.000 0.024 0.000 0.976 0.000
#&gt; SRR1927026     4  0.0146      0.942 0.004 0.000 0.000 0.996 0.000 0.000
#&gt; SRR1927024     4  0.2997      0.826 0.060 0.000 0.000 0.844 0.000 0.096
#&gt; SRR1927025     2  0.4297      0.556 0.000 0.756 0.016 0.000 0.096 0.132
#&gt; SRR1927023     5  0.2378      0.839 0.000 0.000 0.000 0.000 0.848 0.152
#&gt; SRR1927022     1  0.3821      0.640 0.740 0.000 0.000 0.220 0.000 0.040
#&gt; SRR1927021     2  0.3024      0.636 0.000 0.840 0.016 0.000 0.016 0.128
#&gt; SRR1927020     4  0.0291      0.942 0.004 0.000 0.000 0.992 0.000 0.004
#&gt; SRR1927019     6  0.3133      0.846 0.000 0.212 0.008 0.000 0.000 0.780
#&gt; SRR1927071     4  0.0146      0.942 0.004 0.000 0.000 0.996 0.000 0.000
#&gt; SRR1927069     2  0.0632      0.724 0.000 0.976 0.000 0.000 0.000 0.024
#&gt; SRR1927070     1  0.0146      0.969 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; SRR1927068     4  0.0291      0.942 0.004 0.000 0.000 0.992 0.000 0.004
#&gt; SRR1927066     4  0.0260      0.943 0.008 0.000 0.000 0.992 0.000 0.000
#&gt; SRR1927065     3  0.1461      0.884 0.000 0.016 0.940 0.000 0.000 0.044
#&gt; SRR1927067     3  0.1088      0.900 0.000 0.016 0.960 0.000 0.000 0.024
#&gt; SRR1927064     1  0.0000      0.970 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927063     6  0.3023      0.847 0.000 0.212 0.004 0.000 0.000 0.784
#&gt; SRR1927062     4  0.3198      0.598 0.260 0.000 0.000 0.740 0.000 0.000
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-5-a').click(function(){
  $('#tab-SD-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-SD-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-signatures'>
<ul>
<li><a href='#tab-SD-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-1-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-1"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-2-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-2"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-3-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-3"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-4-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-4"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-5-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-mclust-signature_compare](figure_cola/SD-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-SD-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-mclust-collect-classes](figure_cola/SD-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:NMF**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "NMF"]
# you can also extract it by
# res = res_list["SD:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16868 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-NMF-collect-plots](figure_cola/SD-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-NMF-select-partition-number](figure_cola/SD-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5095 0.491   0.491
#> 3 3 0.842           0.819       0.914         0.1226 0.946   0.889
#> 4 4 0.633           0.524       0.770         0.1448 0.907   0.792
#> 5 5 0.645           0.748       0.803         0.1145 0.772   0.440
#> 6 6 0.668           0.779       0.823         0.0464 0.952   0.804
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-classes'>
<ul>
<li><a href='#tab-SD-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-NMF-get-classes-1'>
<p><a id='tab-SD-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1927048     1       0          1  1  0
#&gt; SRR1927061     2       0          1  0  1
#&gt; SRR1927060     1       0          1  1  0
#&gt; SRR1927059     2       0          1  0  1
#&gt; SRR1927058     1       0          1  1  0
#&gt; SRR1927057     2       0          1  0  1
#&gt; SRR1927055     2       0          1  0  1
#&gt; SRR1927056     1       0          1  1  0
#&gt; SRR1927054     1       0          1  1  0
#&gt; SRR1927052     1       0          1  1  0
#&gt; SRR1927053     2       0          1  0  1
#&gt; SRR1927051     2       0          1  0  1
#&gt; SRR1927050     1       0          1  1  0
#&gt; SRR1927049     2       0          1  0  1
#&gt; SRR1927047     2       0          1  0  1
#&gt; SRR1927046     1       0          1  1  0
#&gt; SRR1927045     2       0          1  0  1
#&gt; SRR1927044     1       0          1  1  0
#&gt; SRR1927043     2       0          1  0  1
#&gt; SRR1927042     1       0          1  1  0
#&gt; SRR1927040     1       0          1  1  0
#&gt; SRR1927039     2       0          1  0  1
#&gt; SRR1927038     1       0          1  1  0
#&gt; SRR1927037     2       0          1  0  1
#&gt; SRR1927036     1       0          1  1  0
#&gt; SRR1927035     2       0          1  0  1
#&gt; SRR1927034     1       0          1  1  0
#&gt; SRR1927033     2       0          1  0  1
#&gt; SRR1927032     1       0          1  1  0
#&gt; SRR1927031     2       0          1  0  1
#&gt; SRR1927030     1       0          1  1  0
#&gt; SRR1927028     1       0          1  1  0
#&gt; SRR1927029     2       0          1  0  1
#&gt; SRR1927027     2       0          1  0  1
#&gt; SRR1927026     1       0          1  1  0
#&gt; SRR1927024     1       0          1  1  0
#&gt; SRR1927025     2       0          1  0  1
#&gt; SRR1927023     2       0          1  0  1
#&gt; SRR1927022     1       0          1  1  0
#&gt; SRR1927021     2       0          1  0  1
#&gt; SRR1927020     1       0          1  1  0
#&gt; SRR1927019     2       0          1  0  1
#&gt; SRR1927071     1       0          1  1  0
#&gt; SRR1927069     2       0          1  0  1
#&gt; SRR1927070     1       0          1  1  0
#&gt; SRR1927068     1       0          1  1  0
#&gt; SRR1927066     1       0          1  1  0
#&gt; SRR1927065     2       0          1  0  1
#&gt; SRR1927067     2       0          1  0  1
#&gt; SRR1927064     1       0          1  1  0
#&gt; SRR1927063     2       0          1  0  1
#&gt; SRR1927062     1       0          1  1  0
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-1-a').click(function(){
  $('#tab-SD-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-2'>
<p><a id='tab-SD-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1927048     1  0.5785     -0.113 0.668 0.000 0.332
#&gt; SRR1927061     2  0.0000      0.961 0.000 1.000 0.000
#&gt; SRR1927060     3  0.6274      0.881 0.456 0.000 0.544
#&gt; SRR1927059     2  0.4178      0.802 0.000 0.828 0.172
#&gt; SRR1927058     1  0.3116      0.781 0.892 0.000 0.108
#&gt; SRR1927057     2  0.0000      0.961 0.000 1.000 0.000
#&gt; SRR1927055     2  0.0000      0.961 0.000 1.000 0.000
#&gt; SRR1927056     1  0.0000      0.851 1.000 0.000 0.000
#&gt; SRR1927054     1  0.6079     -0.437 0.612 0.000 0.388
#&gt; SRR1927052     1  0.0000      0.851 1.000 0.000 0.000
#&gt; SRR1927053     2  0.5926      0.570 0.000 0.644 0.356
#&gt; SRR1927051     2  0.0000      0.961 0.000 1.000 0.000
#&gt; SRR1927050     1  0.0000      0.851 1.000 0.000 0.000
#&gt; SRR1927049     2  0.0000      0.961 0.000 1.000 0.000
#&gt; SRR1927047     2  0.0000      0.961 0.000 1.000 0.000
#&gt; SRR1927046     1  0.2711      0.806 0.912 0.000 0.088
#&gt; SRR1927045     2  0.0000      0.961 0.000 1.000 0.000
#&gt; SRR1927044     1  0.2448      0.819 0.924 0.000 0.076
#&gt; SRR1927043     2  0.0000      0.961 0.000 1.000 0.000
#&gt; SRR1927042     1  0.3619      0.733 0.864 0.000 0.136
#&gt; SRR1927040     3  0.6307      0.834 0.488 0.000 0.512
#&gt; SRR1927039     2  0.6302      0.360 0.000 0.520 0.480
#&gt; SRR1927038     3  0.6079      0.824 0.388 0.000 0.612
#&gt; SRR1927037     2  0.0000      0.961 0.000 1.000 0.000
#&gt; SRR1927036     1  0.2448      0.819 0.924 0.000 0.076
#&gt; SRR1927035     2  0.0000      0.961 0.000 1.000 0.000
#&gt; SRR1927034     1  0.1031      0.822 0.976 0.000 0.024
#&gt; SRR1927033     2  0.0000      0.961 0.000 1.000 0.000
#&gt; SRR1927032     1  0.4974      0.445 0.764 0.000 0.236
#&gt; SRR1927031     2  0.0000      0.961 0.000 1.000 0.000
#&gt; SRR1927030     1  0.2448      0.819 0.924 0.000 0.076
#&gt; SRR1927028     1  0.0000      0.851 1.000 0.000 0.000
#&gt; SRR1927029     2  0.0000      0.961 0.000 1.000 0.000
#&gt; SRR1927027     2  0.0000      0.961 0.000 1.000 0.000
#&gt; SRR1927026     1  0.0000      0.851 1.000 0.000 0.000
#&gt; SRR1927024     1  0.0000      0.851 1.000 0.000 0.000
#&gt; SRR1927025     2  0.0000      0.961 0.000 1.000 0.000
#&gt; SRR1927023     2  0.0000      0.961 0.000 1.000 0.000
#&gt; SRR1927022     1  0.0892      0.846 0.980 0.000 0.020
#&gt; SRR1927021     2  0.0000      0.961 0.000 1.000 0.000
#&gt; SRR1927020     1  0.0000      0.851 1.000 0.000 0.000
#&gt; SRR1927019     2  0.0000      0.961 0.000 1.000 0.000
#&gt; SRR1927071     1  0.0000      0.851 1.000 0.000 0.000
#&gt; SRR1927069     2  0.0000      0.961 0.000 1.000 0.000
#&gt; SRR1927070     1  0.2448      0.819 0.924 0.000 0.076
#&gt; SRR1927068     1  0.0000      0.851 1.000 0.000 0.000
#&gt; SRR1927066     1  0.0000      0.851 1.000 0.000 0.000
#&gt; SRR1927065     2  0.0000      0.961 0.000 1.000 0.000
#&gt; SRR1927067     2  0.0000      0.961 0.000 1.000 0.000
#&gt; SRR1927064     1  0.4235      0.642 0.824 0.000 0.176
#&gt; SRR1927063     2  0.0000      0.961 0.000 1.000 0.000
#&gt; SRR1927062     1  0.0000      0.851 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-2-a').click(function(){
  $('#tab-SD-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-3'>
<p><a id='tab-SD-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1927048     1  0.4996     0.2573 0.516 0.000 0.000 0.484
#&gt; SRR1927061     2  0.3311     0.6903 0.000 0.828 0.172 0.000
#&gt; SRR1927060     1  0.4843     0.4737 0.604 0.000 0.000 0.396
#&gt; SRR1927059     2  0.4535     0.5687 0.084 0.804 0.112 0.000
#&gt; SRR1927058     4  0.4585     0.4195 0.332 0.000 0.000 0.668
#&gt; SRR1927057     2  0.0469     0.7382 0.000 0.988 0.012 0.000
#&gt; SRR1927055     2  0.3400     0.6854 0.000 0.820 0.180 0.000
#&gt; SRR1927056     4  0.0000     0.7123 0.000 0.000 0.000 1.000
#&gt; SRR1927054     1  0.4992     0.3039 0.524 0.000 0.000 0.476
#&gt; SRR1927052     4  0.0000     0.7123 0.000 0.000 0.000 1.000
#&gt; SRR1927053     2  0.6968     0.0128 0.308 0.552 0.140 0.000
#&gt; SRR1927051     2  0.0592     0.7345 0.000 0.984 0.016 0.000
#&gt; SRR1927050     4  0.0000     0.7123 0.000 0.000 0.000 1.000
#&gt; SRR1927049     2  0.0336     0.7366 0.000 0.992 0.008 0.000
#&gt; SRR1927047     2  0.4114     0.6015 0.060 0.828 0.112 0.000
#&gt; SRR1927046     4  0.4477     0.4487 0.312 0.000 0.000 0.688
#&gt; SRR1927045     2  0.3266     0.6944 0.000 0.832 0.168 0.000
#&gt; SRR1927044     4  0.4564     0.4286 0.328 0.000 0.000 0.672
#&gt; SRR1927043     2  0.3400     0.6854 0.000 0.820 0.180 0.000
#&gt; SRR1927042     4  0.4679     0.3636 0.352 0.000 0.000 0.648
#&gt; SRR1927040     1  0.4866     0.4669 0.596 0.000 0.000 0.404
#&gt; SRR1927039     1  0.7252    -0.5449 0.436 0.420 0.144 0.000
#&gt; SRR1927038     1  0.4406     0.4564 0.700 0.000 0.000 0.300
#&gt; SRR1927037     2  0.0779     0.7328 0.004 0.980 0.016 0.000
#&gt; SRR1927036     4  0.4543     0.4345 0.324 0.000 0.000 0.676
#&gt; SRR1927035     2  0.0592     0.7345 0.000 0.984 0.016 0.000
#&gt; SRR1927034     4  0.0000     0.7123 0.000 0.000 0.000 1.000
#&gt; SRR1927033     2  0.4040     0.6140 0.000 0.752 0.248 0.000
#&gt; SRR1927032     4  0.4916     0.0483 0.424 0.000 0.000 0.576
#&gt; SRR1927031     2  0.2611     0.6712 0.008 0.896 0.096 0.000
#&gt; SRR1927030     4  0.4564     0.4286 0.328 0.000 0.000 0.672
#&gt; SRR1927028     4  0.0000     0.7123 0.000 0.000 0.000 1.000
#&gt; SRR1927029     2  0.3400     0.6854 0.000 0.820 0.180 0.000
#&gt; SRR1927027     3  0.4164     0.4960 0.000 0.264 0.736 0.000
#&gt; SRR1927026     4  0.0000     0.7123 0.000 0.000 0.000 1.000
#&gt; SRR1927024     4  0.3172     0.5033 0.000 0.000 0.160 0.840
#&gt; SRR1927025     2  0.4998    -0.3520 0.000 0.512 0.488 0.000
#&gt; SRR1927023     3  0.4277     0.5407 0.000 0.280 0.720 0.000
#&gt; SRR1927022     4  0.0592     0.7070 0.016 0.000 0.000 0.984
#&gt; SRR1927021     2  0.5151    -0.2703 0.004 0.532 0.464 0.000
#&gt; SRR1927020     4  0.0000     0.7123 0.000 0.000 0.000 1.000
#&gt; SRR1927019     2  0.0000     0.7374 0.000 1.000 0.000 0.000
#&gt; SRR1927071     4  0.0000     0.7123 0.000 0.000 0.000 1.000
#&gt; SRR1927069     2  0.2149     0.6853 0.000 0.912 0.088 0.000
#&gt; SRR1927070     4  0.4564     0.4286 0.328 0.000 0.000 0.672
#&gt; SRR1927068     4  0.0000     0.7123 0.000 0.000 0.000 1.000
#&gt; SRR1927066     4  0.0188     0.7115 0.004 0.000 0.000 0.996
#&gt; SRR1927065     2  0.3400     0.6854 0.000 0.820 0.180 0.000
#&gt; SRR1927067     2  0.3400     0.6854 0.000 0.820 0.180 0.000
#&gt; SRR1927064     4  0.4713     0.3382 0.360 0.000 0.000 0.640
#&gt; SRR1927063     2  0.0469     0.7382 0.000 0.988 0.012 0.000
#&gt; SRR1927062     4  0.2647     0.6439 0.120 0.000 0.000 0.880
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-3-a').click(function(){
  $('#tab-SD-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-4'>
<p><a id='tab-SD-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1927048     1  0.2813    0.85205 0.832 0.000 0.000 0.168 0.000
#&gt; SRR1927061     2  0.4560   -0.67881 0.000 0.508 0.484 0.000 0.008
#&gt; SRR1927060     1  0.3305    0.90749 0.776 0.000 0.000 0.224 0.000
#&gt; SRR1927059     2  0.1365    0.76743 0.040 0.952 0.004 0.000 0.004
#&gt; SRR1927058     1  0.3895    0.90923 0.680 0.000 0.000 0.320 0.000
#&gt; SRR1927057     2  0.1764    0.74561 0.000 0.928 0.064 0.000 0.008
#&gt; SRR1927055     3  0.4956    0.88364 0.000 0.316 0.636 0.000 0.048
#&gt; SRR1927056     4  0.0162    0.89486 0.004 0.000 0.000 0.996 0.000
#&gt; SRR1927054     1  0.3395    0.91403 0.764 0.000 0.000 0.236 0.000
#&gt; SRR1927052     4  0.0290    0.89291 0.008 0.000 0.000 0.992 0.000
#&gt; SRR1927053     2  0.4220    0.57122 0.180 0.768 0.048 0.000 0.004
#&gt; SRR1927051     2  0.1124    0.77124 0.000 0.960 0.036 0.000 0.004
#&gt; SRR1927050     4  0.0162    0.89192 0.000 0.000 0.004 0.996 0.000
#&gt; SRR1927049     2  0.1197    0.76444 0.000 0.952 0.048 0.000 0.000
#&gt; SRR1927047     2  0.2316    0.75240 0.036 0.916 0.036 0.000 0.012
#&gt; SRR1927046     1  0.3913    0.90265 0.676 0.000 0.000 0.324 0.000
#&gt; SRR1927045     3  0.4787    0.81120 0.000 0.432 0.548 0.000 0.020
#&gt; SRR1927044     1  0.3932    0.90431 0.672 0.000 0.000 0.328 0.000
#&gt; SRR1927043     3  0.4045    0.90855 0.000 0.356 0.644 0.000 0.000
#&gt; SRR1927042     1  0.3661    0.92189 0.724 0.000 0.000 0.276 0.000
#&gt; SRR1927040     1  0.3210    0.89881 0.788 0.000 0.000 0.212 0.000
#&gt; SRR1927039     2  0.4897    0.53087 0.172 0.744 0.048 0.000 0.036
#&gt; SRR1927038     1  0.3003    0.87678 0.812 0.000 0.000 0.188 0.000
#&gt; SRR1927037     2  0.1251    0.76830 0.000 0.956 0.036 0.000 0.008
#&gt; SRR1927036     1  0.3966    0.89699 0.664 0.000 0.000 0.336 0.000
#&gt; SRR1927035     2  0.1043    0.76928 0.000 0.960 0.040 0.000 0.000
#&gt; SRR1927034     4  0.2970    0.72180 0.000 0.000 0.168 0.828 0.004
#&gt; SRR1927033     3  0.5365    0.82262 0.000 0.284 0.628 0.000 0.088
#&gt; SRR1927032     1  0.3612    0.92201 0.732 0.000 0.000 0.268 0.000
#&gt; SRR1927031     2  0.1857    0.74873 0.008 0.928 0.004 0.000 0.060
#&gt; SRR1927030     1  0.3949    0.90084 0.668 0.000 0.000 0.332 0.000
#&gt; SRR1927028     4  0.0000    0.89352 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927029     3  0.3999    0.90535 0.000 0.344 0.656 0.000 0.000
#&gt; SRR1927027     5  0.5074    0.43333 0.000 0.072 0.268 0.000 0.660
#&gt; SRR1927026     4  0.0162    0.89486 0.004 0.000 0.000 0.996 0.000
#&gt; SRR1927024     4  0.3728    0.67099 0.000 0.000 0.008 0.748 0.244
#&gt; SRR1927025     5  0.4390    0.31886 0.000 0.428 0.004 0.000 0.568
#&gt; SRR1927023     5  0.2605    0.63979 0.000 0.148 0.000 0.000 0.852
#&gt; SRR1927022     4  0.4126   -0.15287 0.380 0.000 0.000 0.620 0.000
#&gt; SRR1927021     2  0.4874    0.00869 0.000 0.600 0.032 0.000 0.368
#&gt; SRR1927020     4  0.0324    0.89390 0.004 0.000 0.004 0.992 0.000
#&gt; SRR1927019     2  0.1251    0.76898 0.000 0.956 0.036 0.000 0.008
#&gt; SRR1927071     4  0.0162    0.89486 0.004 0.000 0.000 0.996 0.000
#&gt; SRR1927069     2  0.2761    0.69408 0.000 0.872 0.024 0.000 0.104
#&gt; SRR1927070     1  0.3932    0.90431 0.672 0.000 0.000 0.328 0.000
#&gt; SRR1927068     4  0.0162    0.89486 0.004 0.000 0.000 0.996 0.000
#&gt; SRR1927066     4  0.0290    0.89291 0.008 0.000 0.000 0.992 0.000
#&gt; SRR1927065     3  0.4192    0.87556 0.000 0.404 0.596 0.000 0.000
#&gt; SRR1927067     3  0.4060    0.90195 0.000 0.360 0.640 0.000 0.000
#&gt; SRR1927064     1  0.3508    0.91984 0.748 0.000 0.000 0.252 0.000
#&gt; SRR1927063     2  0.2193    0.70649 0.000 0.900 0.092 0.000 0.008
#&gt; SRR1927062     4  0.2616    0.77907 0.100 0.000 0.020 0.880 0.000
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-4-a').click(function(){
  $('#tab-SD-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-5'>
<p><a id='tab-SD-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1927048     1  0.1564      0.917 0.936 0.000 0.000 0.024 0.000 0.040
#&gt; SRR1927061     3  0.4057      0.551 0.000 0.436 0.556 0.000 0.000 0.008
#&gt; SRR1927060     1  0.0291      0.926 0.992 0.000 0.000 0.004 0.000 0.004
#&gt; SRR1927059     2  0.3326      0.750 0.016 0.848 0.012 0.000 0.084 0.040
#&gt; SRR1927058     1  0.1327      0.922 0.936 0.000 0.000 0.064 0.000 0.000
#&gt; SRR1927057     2  0.3240      0.731 0.000 0.820 0.144 0.000 0.008 0.028
#&gt; SRR1927055     3  0.3020      0.774 0.000 0.156 0.824 0.000 0.012 0.008
#&gt; SRR1927056     4  0.2302      0.904 0.120 0.000 0.000 0.872 0.000 0.008
#&gt; SRR1927054     1  0.0260      0.928 0.992 0.000 0.000 0.008 0.000 0.000
#&gt; SRR1927052     4  0.2278      0.904 0.128 0.000 0.000 0.868 0.000 0.004
#&gt; SRR1927053     2  0.4849      0.619 0.056 0.740 0.008 0.000 0.128 0.068
#&gt; SRR1927051     2  0.1700      0.796 0.000 0.916 0.080 0.000 0.004 0.000
#&gt; SRR1927050     4  0.2618      0.902 0.116 0.000 0.000 0.860 0.000 0.024
#&gt; SRR1927049     2  0.2442      0.747 0.000 0.852 0.144 0.000 0.000 0.004
#&gt; SRR1927047     2  0.2457      0.802 0.008 0.904 0.028 0.000 0.032 0.028
#&gt; SRR1927046     1  0.1765      0.919 0.924 0.000 0.000 0.052 0.000 0.024
#&gt; SRR1927045     3  0.3357      0.787 0.000 0.224 0.764 0.000 0.008 0.004
#&gt; SRR1927044     1  0.1267      0.922 0.940 0.000 0.000 0.060 0.000 0.000
#&gt; SRR1927043     3  0.2969      0.799 0.000 0.224 0.776 0.000 0.000 0.000
#&gt; SRR1927042     1  0.0260      0.928 0.992 0.000 0.000 0.008 0.000 0.000
#&gt; SRR1927040     1  0.0508      0.922 0.984 0.000 0.000 0.004 0.000 0.012
#&gt; SRR1927039     2  0.4752      0.607 0.048 0.740 0.008 0.000 0.148 0.056
#&gt; SRR1927038     1  0.0922      0.912 0.968 0.004 0.000 0.004 0.000 0.024
#&gt; SRR1927037     2  0.1989      0.799 0.000 0.916 0.052 0.000 0.004 0.028
#&gt; SRR1927036     1  0.1610      0.908 0.916 0.000 0.000 0.084 0.000 0.000
#&gt; SRR1927035     2  0.2454      0.795 0.000 0.884 0.088 0.000 0.020 0.008
#&gt; SRR1927034     4  0.2737      0.788 0.044 0.000 0.004 0.868 0.000 0.084
#&gt; SRR1927033     3  0.4667      0.677 0.000 0.140 0.728 0.000 0.108 0.024
#&gt; SRR1927032     1  0.0547      0.930 0.980 0.000 0.000 0.020 0.000 0.000
#&gt; SRR1927031     2  0.3172      0.703 0.000 0.820 0.016 0.000 0.152 0.012
#&gt; SRR1927030     1  0.1327      0.921 0.936 0.000 0.000 0.064 0.000 0.000
#&gt; SRR1927028     4  0.2784      0.902 0.124 0.000 0.000 0.848 0.000 0.028
#&gt; SRR1927029     3  0.2520      0.773 0.000 0.152 0.844 0.000 0.000 0.004
#&gt; SRR1927027     5  0.6026      0.367 0.000 0.068 0.256 0.000 0.576 0.100
#&gt; SRR1927026     4  0.3586      0.885 0.128 0.000 0.000 0.812 0.032 0.028
#&gt; SRR1927024     4  0.6770      0.431 0.092 0.000 0.000 0.464 0.304 0.140
#&gt; SRR1927025     5  0.3686      0.671 0.000 0.220 0.000 0.000 0.748 0.032
#&gt; SRR1927023     5  0.1957      0.680 0.000 0.112 0.000 0.000 0.888 0.000
#&gt; SRR1927022     1  0.5042      0.349 0.612 0.000 0.000 0.316 0.040 0.032
#&gt; SRR1927021     5  0.5270      0.368 0.000 0.404 0.000 0.000 0.496 0.100
#&gt; SRR1927020     4  0.2288      0.902 0.116 0.000 0.004 0.876 0.000 0.004
#&gt; SRR1927019     2  0.2121      0.782 0.000 0.892 0.096 0.000 0.000 0.012
#&gt; SRR1927071     4  0.2706      0.903 0.124 0.000 0.000 0.852 0.000 0.024
#&gt; SRR1927069     2  0.3106      0.739 0.000 0.840 0.016 0.000 0.120 0.024
#&gt; SRR1927070     1  0.1556      0.914 0.920 0.000 0.000 0.080 0.000 0.000
#&gt; SRR1927068     4  0.2673      0.899 0.132 0.000 0.004 0.852 0.000 0.012
#&gt; SRR1927066     4  0.2572      0.900 0.136 0.000 0.000 0.852 0.000 0.012
#&gt; SRR1927065     3  0.4070      0.598 0.000 0.424 0.568 0.000 0.004 0.004
#&gt; SRR1927067     3  0.4214      0.727 0.000 0.320 0.652 0.000 0.004 0.024
#&gt; SRR1927064     1  0.1245      0.922 0.952 0.000 0.000 0.016 0.000 0.032
#&gt; SRR1927063     2  0.3136      0.664 0.000 0.796 0.188 0.000 0.000 0.016
#&gt; SRR1927062     4  0.4513      0.632 0.324 0.000 0.024 0.636 0.000 0.016
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-5-a').click(function(){
  $('#tab-SD-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-SD-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-signatures'>
<ul>
<li><a href='#tab-SD-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-1-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-1"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-2-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-2"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-3-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-3"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-4-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-4"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-5-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-NMF-signature_compare](figure_cola/SD-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-SD-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-NMF-collect-classes](figure_cola/SD-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:hclust*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "hclust"]
# you can also extract it by
# res = res_list["CV:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16868 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-hclust-collect-plots](figure_cola/CV-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-hclust-select-partition-number](figure_cola/CV-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5095 0.491   0.491
#> 3 3 1.000           0.975       0.991         0.0840 0.950   0.899
#> 4 4 0.921           0.931       0.951         0.1555 0.921   0.821
#> 5 5 0.843           0.867       0.937         0.2040 0.863   0.621
#> 6 6 0.784           0.722       0.845         0.0479 0.967   0.852
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
#> attr(,"optional")
#> [1] 2 3
```

There is also optional best $k$ = 2 3 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-classes'>
<ul>
<li><a href='#tab-CV-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-hclust-get-classes-1'>
<p><a id='tab-CV-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1927048     1       0          1  1  0
#&gt; SRR1927061     2       0          1  0  1
#&gt; SRR1927060     1       0          1  1  0
#&gt; SRR1927059     2       0          1  0  1
#&gt; SRR1927058     1       0          1  1  0
#&gt; SRR1927057     2       0          1  0  1
#&gt; SRR1927055     2       0          1  0  1
#&gt; SRR1927056     1       0          1  1  0
#&gt; SRR1927054     1       0          1  1  0
#&gt; SRR1927052     1       0          1  1  0
#&gt; SRR1927053     2       0          1  0  1
#&gt; SRR1927051     2       0          1  0  1
#&gt; SRR1927050     1       0          1  1  0
#&gt; SRR1927049     2       0          1  0  1
#&gt; SRR1927047     2       0          1  0  1
#&gt; SRR1927046     1       0          1  1  0
#&gt; SRR1927045     2       0          1  0  1
#&gt; SRR1927044     1       0          1  1  0
#&gt; SRR1927043     2       0          1  0  1
#&gt; SRR1927042     1       0          1  1  0
#&gt; SRR1927040     1       0          1  1  0
#&gt; SRR1927039     2       0          1  0  1
#&gt; SRR1927038     1       0          1  1  0
#&gt; SRR1927037     2       0          1  0  1
#&gt; SRR1927036     1       0          1  1  0
#&gt; SRR1927035     2       0          1  0  1
#&gt; SRR1927034     1       0          1  1  0
#&gt; SRR1927033     2       0          1  0  1
#&gt; SRR1927032     1       0          1  1  0
#&gt; SRR1927031     2       0          1  0  1
#&gt; SRR1927030     1       0          1  1  0
#&gt; SRR1927028     1       0          1  1  0
#&gt; SRR1927029     2       0          1  0  1
#&gt; SRR1927027     2       0          1  0  1
#&gt; SRR1927026     1       0          1  1  0
#&gt; SRR1927024     1       0          1  1  0
#&gt; SRR1927025     2       0          1  0  1
#&gt; SRR1927023     2       0          1  0  1
#&gt; SRR1927022     1       0          1  1  0
#&gt; SRR1927021     2       0          1  0  1
#&gt; SRR1927020     1       0          1  1  0
#&gt; SRR1927019     2       0          1  0  1
#&gt; SRR1927071     1       0          1  1  0
#&gt; SRR1927069     2       0          1  0  1
#&gt; SRR1927070     1       0          1  1  0
#&gt; SRR1927068     1       0          1  1  0
#&gt; SRR1927066     1       0          1  1  0
#&gt; SRR1927065     2       0          1  0  1
#&gt; SRR1927067     2       0          1  0  1
#&gt; SRR1927064     1       0          1  1  0
#&gt; SRR1927063     2       0          1  0  1
#&gt; SRR1927062     1       0          1  1  0
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-1-a').click(function(){
  $('#tab-CV-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-2'>
<p><a id='tab-CV-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1   p2   p3
#&gt; SRR1927048     1   0.000      1.000  1 0.00 0.00
#&gt; SRR1927061     2   0.000      1.000  0 1.00 0.00
#&gt; SRR1927060     1   0.000      1.000  1 0.00 0.00
#&gt; SRR1927059     2   0.000      1.000  0 1.00 0.00
#&gt; SRR1927058     1   0.000      1.000  1 0.00 0.00
#&gt; SRR1927057     2   0.000      1.000  0 1.00 0.00
#&gt; SRR1927055     2   0.000      1.000  0 1.00 0.00
#&gt; SRR1927056     1   0.000      1.000  1 0.00 0.00
#&gt; SRR1927054     1   0.000      1.000  1 0.00 0.00
#&gt; SRR1927052     1   0.000      1.000  1 0.00 0.00
#&gt; SRR1927053     2   0.000      1.000  0 1.00 0.00
#&gt; SRR1927051     2   0.000      1.000  0 1.00 0.00
#&gt; SRR1927050     1   0.000      1.000  1 0.00 0.00
#&gt; SRR1927049     2   0.000      1.000  0 1.00 0.00
#&gt; SRR1927047     2   0.000      1.000  0 1.00 0.00
#&gt; SRR1927046     1   0.000      1.000  1 0.00 0.00
#&gt; SRR1927045     2   0.000      1.000  0 1.00 0.00
#&gt; SRR1927044     1   0.000      1.000  1 0.00 0.00
#&gt; SRR1927043     2   0.000      1.000  0 1.00 0.00
#&gt; SRR1927042     1   0.000      1.000  1 0.00 0.00
#&gt; SRR1927040     1   0.000      1.000  1 0.00 0.00
#&gt; SRR1927039     2   0.000      1.000  0 1.00 0.00
#&gt; SRR1927038     1   0.000      1.000  1 0.00 0.00
#&gt; SRR1927037     2   0.000      1.000  0 1.00 0.00
#&gt; SRR1927036     1   0.000      1.000  1 0.00 0.00
#&gt; SRR1927035     2   0.000      1.000  0 1.00 0.00
#&gt; SRR1927034     1   0.000      1.000  1 0.00 0.00
#&gt; SRR1927033     2   0.000      1.000  0 1.00 0.00
#&gt; SRR1927032     1   0.000      1.000  1 0.00 0.00
#&gt; SRR1927031     2   0.000      1.000  0 1.00 0.00
#&gt; SRR1927030     1   0.000      1.000  1 0.00 0.00
#&gt; SRR1927028     1   0.000      1.000  1 0.00 0.00
#&gt; SRR1927029     2   0.000      1.000  0 1.00 0.00
#&gt; SRR1927027     3   0.000      0.765  0 0.00 1.00
#&gt; SRR1927026     1   0.000      1.000  1 0.00 0.00
#&gt; SRR1927024     1   0.000      1.000  1 0.00 0.00
#&gt; SRR1927025     3   0.628      0.148  0 0.46 0.54
#&gt; SRR1927023     3   0.000      0.765  0 0.00 1.00
#&gt; SRR1927022     1   0.000      1.000  1 0.00 0.00
#&gt; SRR1927021     2   0.000      1.000  0 1.00 0.00
#&gt; SRR1927020     1   0.000      1.000  1 0.00 0.00
#&gt; SRR1927019     2   0.000      1.000  0 1.00 0.00
#&gt; SRR1927071     1   0.000      1.000  1 0.00 0.00
#&gt; SRR1927069     2   0.000      1.000  0 1.00 0.00
#&gt; SRR1927070     1   0.000      1.000  1 0.00 0.00
#&gt; SRR1927068     1   0.000      1.000  1 0.00 0.00
#&gt; SRR1927066     1   0.000      1.000  1 0.00 0.00
#&gt; SRR1927065     2   0.000      1.000  0 1.00 0.00
#&gt; SRR1927067     2   0.000      1.000  0 1.00 0.00
#&gt; SRR1927064     1   0.000      1.000  1 0.00 0.00
#&gt; SRR1927063     2   0.000      1.000  0 1.00 0.00
#&gt; SRR1927062     1   0.000      1.000  1 0.00 0.00
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-2-a').click(function(){
  $('#tab-CV-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-3'>
<p><a id='tab-CV-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3   p4
#&gt; SRR1927048     1  0.0000      0.982 1.000 0.000 0.000 0.00
#&gt; SRR1927061     3  0.1557      1.000 0.000 0.056 0.944 0.00
#&gt; SRR1927060     1  0.0000      0.982 1.000 0.000 0.000 0.00
#&gt; SRR1927059     2  0.0000      0.921 0.000 1.000 0.000 0.00
#&gt; SRR1927058     1  0.0000      0.982 1.000 0.000 0.000 0.00
#&gt; SRR1927057     2  0.0921      0.911 0.000 0.972 0.028 0.00
#&gt; SRR1927055     3  0.1557      1.000 0.000 0.056 0.944 0.00
#&gt; SRR1927056     1  0.1557      0.965 0.944 0.000 0.056 0.00
#&gt; SRR1927054     1  0.0000      0.982 1.000 0.000 0.000 0.00
#&gt; SRR1927052     1  0.0469      0.981 0.988 0.000 0.012 0.00
#&gt; SRR1927053     2  0.0000      0.921 0.000 1.000 0.000 0.00
#&gt; SRR1927051     2  0.2760      0.874 0.000 0.872 0.128 0.00
#&gt; SRR1927050     1  0.1557      0.965 0.944 0.000 0.056 0.00
#&gt; SRR1927049     2  0.2760      0.874 0.000 0.872 0.128 0.00
#&gt; SRR1927047     2  0.0000      0.921 0.000 1.000 0.000 0.00
#&gt; SRR1927046     1  0.0000      0.982 1.000 0.000 0.000 0.00
#&gt; SRR1927045     2  0.2281      0.889 0.000 0.904 0.096 0.00
#&gt; SRR1927044     1  0.0000      0.982 1.000 0.000 0.000 0.00
#&gt; SRR1927043     3  0.1557      1.000 0.000 0.056 0.944 0.00
#&gt; SRR1927042     1  0.0000      0.982 1.000 0.000 0.000 0.00
#&gt; SRR1927040     1  0.0000      0.982 1.000 0.000 0.000 0.00
#&gt; SRR1927039     2  0.0000      0.921 0.000 1.000 0.000 0.00
#&gt; SRR1927038     1  0.0000      0.982 1.000 0.000 0.000 0.00
#&gt; SRR1927037     2  0.0188      0.921 0.000 0.996 0.004 0.00
#&gt; SRR1927036     1  0.0188      0.982 0.996 0.000 0.004 0.00
#&gt; SRR1927035     2  0.2760      0.874 0.000 0.872 0.128 0.00
#&gt; SRR1927034     1  0.1557      0.965 0.944 0.000 0.056 0.00
#&gt; SRR1927033     3  0.1557      1.000 0.000 0.056 0.944 0.00
#&gt; SRR1927032     1  0.0000      0.982 1.000 0.000 0.000 0.00
#&gt; SRR1927031     2  0.0000      0.921 0.000 1.000 0.000 0.00
#&gt; SRR1927030     1  0.0000      0.982 1.000 0.000 0.000 0.00
#&gt; SRR1927028     1  0.1557      0.965 0.944 0.000 0.056 0.00
#&gt; SRR1927029     3  0.1557      1.000 0.000 0.056 0.944 0.00
#&gt; SRR1927027     4  0.0000      0.704 0.000 0.000 0.000 1.00
#&gt; SRR1927026     1  0.1557      0.965 0.944 0.000 0.056 0.00
#&gt; SRR1927024     1  0.0469      0.981 0.988 0.000 0.012 0.00
#&gt; SRR1927025     4  0.4977      0.177 0.000 0.460 0.000 0.54
#&gt; SRR1927023     4  0.0000      0.704 0.000 0.000 0.000 1.00
#&gt; SRR1927022     1  0.0592      0.980 0.984 0.000 0.016 0.00
#&gt; SRR1927021     2  0.0000      0.921 0.000 1.000 0.000 0.00
#&gt; SRR1927020     1  0.1557      0.965 0.944 0.000 0.056 0.00
#&gt; SRR1927019     2  0.2760      0.874 0.000 0.872 0.128 0.00
#&gt; SRR1927071     1  0.1557      0.965 0.944 0.000 0.056 0.00
#&gt; SRR1927069     2  0.0000      0.921 0.000 1.000 0.000 0.00
#&gt; SRR1927070     1  0.0000      0.982 1.000 0.000 0.000 0.00
#&gt; SRR1927068     1  0.1557      0.965 0.944 0.000 0.056 0.00
#&gt; SRR1927066     1  0.0707      0.979 0.980 0.000 0.020 0.00
#&gt; SRR1927065     3  0.1557      1.000 0.000 0.056 0.944 0.00
#&gt; SRR1927067     3  0.1557      1.000 0.000 0.056 0.944 0.00
#&gt; SRR1927064     1  0.0000      0.982 1.000 0.000 0.000 0.00
#&gt; SRR1927063     2  0.3569      0.797 0.000 0.804 0.196 0.00
#&gt; SRR1927062     1  0.0592      0.980 0.984 0.000 0.016 0.00
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-3-a').click(function(){
  $('#tab-CV-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-4'>
<p><a id='tab-CV-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4   p5
#&gt; SRR1927048     1  0.0000      0.972 1.000 0.000 0.000 0.000 0.00
#&gt; SRR1927061     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.00
#&gt; SRR1927060     1  0.0000      0.972 1.000 0.000 0.000 0.000 0.00
#&gt; SRR1927059     2  0.0000      0.902 0.000 1.000 0.000 0.000 0.00
#&gt; SRR1927058     1  0.0162      0.971 0.996 0.000 0.000 0.004 0.00
#&gt; SRR1927057     2  0.0880      0.889 0.000 0.968 0.032 0.000 0.00
#&gt; SRR1927055     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.00
#&gt; SRR1927056     4  0.0000      0.838 0.000 0.000 0.000 1.000 0.00
#&gt; SRR1927054     1  0.0000      0.972 1.000 0.000 0.000 0.000 0.00
#&gt; SRR1927052     4  0.4074      0.546 0.364 0.000 0.000 0.636 0.00
#&gt; SRR1927053     2  0.0000      0.902 0.000 1.000 0.000 0.000 0.00
#&gt; SRR1927051     2  0.2732      0.841 0.000 0.840 0.160 0.000 0.00
#&gt; SRR1927050     4  0.0000      0.838 0.000 0.000 0.000 1.000 0.00
#&gt; SRR1927049     2  0.2732      0.841 0.000 0.840 0.160 0.000 0.00
#&gt; SRR1927047     2  0.0000      0.902 0.000 1.000 0.000 0.000 0.00
#&gt; SRR1927046     1  0.0000      0.972 1.000 0.000 0.000 0.000 0.00
#&gt; SRR1927045     2  0.2230      0.863 0.000 0.884 0.116 0.000 0.00
#&gt; SRR1927044     1  0.1197      0.953 0.952 0.000 0.000 0.048 0.00
#&gt; SRR1927043     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.00
#&gt; SRR1927042     1  0.1197      0.953 0.952 0.000 0.000 0.048 0.00
#&gt; SRR1927040     1  0.0000      0.972 1.000 0.000 0.000 0.000 0.00
#&gt; SRR1927039     2  0.0000      0.902 0.000 1.000 0.000 0.000 0.00
#&gt; SRR1927038     1  0.0000      0.972 1.000 0.000 0.000 0.000 0.00
#&gt; SRR1927037     2  0.0162      0.901 0.000 0.996 0.004 0.000 0.00
#&gt; SRR1927036     1  0.2020      0.897 0.900 0.000 0.000 0.100 0.00
#&gt; SRR1927035     2  0.2732      0.841 0.000 0.840 0.160 0.000 0.00
#&gt; SRR1927034     4  0.0000      0.838 0.000 0.000 0.000 1.000 0.00
#&gt; SRR1927033     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.00
#&gt; SRR1927032     1  0.0000      0.972 1.000 0.000 0.000 0.000 0.00
#&gt; SRR1927031     2  0.0000      0.902 0.000 1.000 0.000 0.000 0.00
#&gt; SRR1927030     1  0.1197      0.953 0.952 0.000 0.000 0.048 0.00
#&gt; SRR1927028     4  0.0162      0.837 0.004 0.000 0.000 0.996 0.00
#&gt; SRR1927029     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.00
#&gt; SRR1927027     5  0.0000      0.709 0.000 0.000 0.000 0.000 1.00
#&gt; SRR1927026     4  0.0000      0.838 0.000 0.000 0.000 1.000 0.00
#&gt; SRR1927024     4  0.4074      0.577 0.364 0.000 0.000 0.636 0.00
#&gt; SRR1927025     5  0.4287      0.188 0.000 0.460 0.000 0.000 0.54
#&gt; SRR1927023     5  0.0000      0.709 0.000 0.000 0.000 0.000 1.00
#&gt; SRR1927022     4  0.3816      0.648 0.304 0.000 0.000 0.696 0.00
#&gt; SRR1927021     2  0.0000      0.902 0.000 1.000 0.000 0.000 0.00
#&gt; SRR1927020     4  0.0000      0.838 0.000 0.000 0.000 1.000 0.00
#&gt; SRR1927019     2  0.2732      0.841 0.000 0.840 0.160 0.000 0.00
#&gt; SRR1927071     4  0.0162      0.838 0.004 0.000 0.000 0.996 0.00
#&gt; SRR1927069     2  0.0000      0.902 0.000 1.000 0.000 0.000 0.00
#&gt; SRR1927070     1  0.1197      0.953 0.952 0.000 0.000 0.048 0.00
#&gt; SRR1927068     4  0.0000      0.838 0.000 0.000 0.000 1.000 0.00
#&gt; SRR1927066     4  0.3143      0.748 0.204 0.000 0.000 0.796 0.00
#&gt; SRR1927065     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.00
#&gt; SRR1927067     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.00
#&gt; SRR1927064     1  0.0000      0.972 1.000 0.000 0.000 0.000 0.00
#&gt; SRR1927063     2  0.3366      0.758 0.000 0.768 0.232 0.000 0.00
#&gt; SRR1927062     4  0.3424      0.723 0.240 0.000 0.000 0.760 0.00
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-4-a').click(function(){
  $('#tab-CV-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-5'>
<p><a id='tab-CV-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1927048     1  0.4322     0.5679 0.600 0.000 0.000 0.000 0.372 0.028
#&gt; SRR1927061     3  0.0146     0.9977 0.000 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1927060     1  0.0000     0.9021 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.0000     0.6594 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927058     1  0.0146     0.9022 0.996 0.000 0.000 0.004 0.000 0.000
#&gt; SRR1927057     2  0.0790     0.6364 0.000 0.968 0.032 0.000 0.000 0.000
#&gt; SRR1927055     3  0.0000     0.9969 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927056     4  0.0000     0.8591 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927054     1  0.0000     0.9021 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927052     4  0.3659     0.5020 0.364 0.000 0.000 0.636 0.000 0.000
#&gt; SRR1927053     2  0.0000     0.6594 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927051     2  0.5394     0.0473 0.000 0.568 0.156 0.000 0.000 0.276
#&gt; SRR1927050     4  0.0000     0.8591 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927049     6  0.5440     0.7401 0.000 0.288 0.156 0.000 0.000 0.556
#&gt; SRR1927047     2  0.3756    -0.0437 0.000 0.600 0.000 0.000 0.000 0.400
#&gt; SRR1927046     1  0.4322     0.5679 0.600 0.000 0.000 0.000 0.372 0.028
#&gt; SRR1927045     6  0.5209     0.7419 0.000 0.324 0.112 0.000 0.000 0.564
#&gt; SRR1927044     1  0.1075     0.8955 0.952 0.000 0.000 0.048 0.000 0.000
#&gt; SRR1927043     3  0.0146     0.9977 0.000 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1927042     1  0.1075     0.8955 0.952 0.000 0.000 0.048 0.000 0.000
#&gt; SRR1927040     1  0.0000     0.9021 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927039     2  0.0000     0.6594 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927038     1  0.0000     0.9021 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.0146     0.6584 0.000 0.996 0.004 0.000 0.000 0.000
#&gt; SRR1927036     1  0.1814     0.8534 0.900 0.000 0.000 0.100 0.000 0.000
#&gt; SRR1927035     2  0.5394     0.0473 0.000 0.568 0.156 0.000 0.000 0.276
#&gt; SRR1927034     4  0.0000     0.8591 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927033     3  0.0146     0.9977 0.000 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1927032     1  0.0000     0.9021 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927031     2  0.0000     0.6594 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927030     1  0.1075     0.8955 0.952 0.000 0.000 0.048 0.000 0.000
#&gt; SRR1927028     4  0.0146     0.8581 0.004 0.000 0.000 0.996 0.000 0.000
#&gt; SRR1927029     3  0.0146     0.9977 0.000 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1927027     5  0.3727     0.7259 0.000 0.000 0.000 0.000 0.612 0.388
#&gt; SRR1927026     4  0.0000     0.8591 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927024     4  0.3874     0.5817 0.008 0.000 0.000 0.636 0.356 0.000
#&gt; SRR1927025     5  0.5295     0.1956 0.000 0.440 0.000 0.000 0.460 0.100
#&gt; SRR1927023     5  0.3684     0.7259 0.000 0.000 0.000 0.000 0.628 0.372
#&gt; SRR1927022     4  0.4330     0.6719 0.068 0.000 0.000 0.696 0.236 0.000
#&gt; SRR1927021     6  0.3797     0.5182 0.000 0.420 0.000 0.000 0.000 0.580
#&gt; SRR1927020     4  0.0000     0.8591 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927019     2  0.5394     0.0473 0.000 0.568 0.156 0.000 0.000 0.276
#&gt; SRR1927071     4  0.0146     0.8583 0.004 0.000 0.000 0.996 0.000 0.000
#&gt; SRR1927069     2  0.3351     0.3416 0.000 0.712 0.000 0.000 0.000 0.288
#&gt; SRR1927070     1  0.1075     0.8955 0.952 0.000 0.000 0.048 0.000 0.000
#&gt; SRR1927068     4  0.0000     0.8591 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927066     4  0.2823     0.7339 0.204 0.000 0.000 0.796 0.000 0.000
#&gt; SRR1927065     3  0.0000     0.9969 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927067     3  0.0000     0.9969 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927064     1  0.2446     0.8183 0.864 0.000 0.000 0.000 0.124 0.012
#&gt; SRR1927063     6  0.5630     0.6943 0.000 0.232 0.228 0.000 0.000 0.540
#&gt; SRR1927062     4  0.3076     0.7010 0.240 0.000 0.000 0.760 0.000 0.000
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-5-a').click(function(){
  $('#tab-CV-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-CV-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-signatures'>
<ul>
<li><a href='#tab-CV-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-1-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-1"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-2-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-2"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-3-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-3"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-4-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-4"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-5-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-hclust-signature_compare](figure_cola/CV-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-CV-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-hclust-collect-classes](figure_cola/CV-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:kmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "kmeans"]
# you can also extract it by
# res = res_list["CV:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16868 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-kmeans-collect-plots](figure_cola/CV-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-kmeans-select-partition-number](figure_cola/CV-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5095 0.491   0.491
#> 3 3 0.687           0.801       0.794         0.2335 1.000   1.000
#> 4 4 0.651           0.604       0.754         0.1281 0.769   0.530
#> 5 5 0.634           0.764       0.748         0.0662 0.876   0.583
#> 6 6 0.719           0.787       0.783         0.0521 0.974   0.881
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-classes'>
<ul>
<li><a href='#tab-CV-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-kmeans-get-classes-1'>
<p><a id='tab-CV-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1927048     1       0          1  1  0
#&gt; SRR1927061     2       0          1  0  1
#&gt; SRR1927060     1       0          1  1  0
#&gt; SRR1927059     2       0          1  0  1
#&gt; SRR1927058     1       0          1  1  0
#&gt; SRR1927057     2       0          1  0  1
#&gt; SRR1927055     2       0          1  0  1
#&gt; SRR1927056     1       0          1  1  0
#&gt; SRR1927054     1       0          1  1  0
#&gt; SRR1927052     1       0          1  1  0
#&gt; SRR1927053     2       0          1  0  1
#&gt; SRR1927051     2       0          1  0  1
#&gt; SRR1927050     1       0          1  1  0
#&gt; SRR1927049     2       0          1  0  1
#&gt; SRR1927047     2       0          1  0  1
#&gt; SRR1927046     1       0          1  1  0
#&gt; SRR1927045     2       0          1  0  1
#&gt; SRR1927044     1       0          1  1  0
#&gt; SRR1927043     2       0          1  0  1
#&gt; SRR1927042     1       0          1  1  0
#&gt; SRR1927040     1       0          1  1  0
#&gt; SRR1927039     2       0          1  0  1
#&gt; SRR1927038     1       0          1  1  0
#&gt; SRR1927037     2       0          1  0  1
#&gt; SRR1927036     1       0          1  1  0
#&gt; SRR1927035     2       0          1  0  1
#&gt; SRR1927034     1       0          1  1  0
#&gt; SRR1927033     2       0          1  0  1
#&gt; SRR1927032     1       0          1  1  0
#&gt; SRR1927031     2       0          1  0  1
#&gt; SRR1927030     1       0          1  1  0
#&gt; SRR1927028     1       0          1  1  0
#&gt; SRR1927029     2       0          1  0  1
#&gt; SRR1927027     2       0          1  0  1
#&gt; SRR1927026     1       0          1  1  0
#&gt; SRR1927024     1       0          1  1  0
#&gt; SRR1927025     2       0          1  0  1
#&gt; SRR1927023     2       0          1  0  1
#&gt; SRR1927022     1       0          1  1  0
#&gt; SRR1927021     2       0          1  0  1
#&gt; SRR1927020     1       0          1  1  0
#&gt; SRR1927019     2       0          1  0  1
#&gt; SRR1927071     1       0          1  1  0
#&gt; SRR1927069     2       0          1  0  1
#&gt; SRR1927070     1       0          1  1  0
#&gt; SRR1927068     1       0          1  1  0
#&gt; SRR1927066     1       0          1  1  0
#&gt; SRR1927065     2       0          1  0  1
#&gt; SRR1927067     2       0          1  0  1
#&gt; SRR1927064     1       0          1  1  0
#&gt; SRR1927063     2       0          1  0  1
#&gt; SRR1927062     1       0          1  1  0
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-1-a').click(function(){
  $('#tab-CV-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-2'>
<p><a id='tab-CV-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3
#&gt; SRR1927048     1  0.0000      0.789 1.000 0.000 NA
#&gt; SRR1927061     2  0.6045      0.830 0.000 0.620 NA
#&gt; SRR1927060     1  0.0000      0.789 1.000 0.000 NA
#&gt; SRR1927059     2  0.1411      0.835 0.000 0.964 NA
#&gt; SRR1927058     1  0.0000      0.789 1.000 0.000 NA
#&gt; SRR1927057     2  0.4235      0.866 0.000 0.824 NA
#&gt; SRR1927055     2  0.6079      0.828 0.000 0.612 NA
#&gt; SRR1927056     1  0.6308      0.752 0.508 0.000 NA
#&gt; SRR1927054     1  0.0000      0.789 1.000 0.000 NA
#&gt; SRR1927052     1  0.6308      0.752 0.508 0.000 NA
#&gt; SRR1927053     2  0.1411      0.835 0.000 0.964 NA
#&gt; SRR1927051     2  0.4291      0.865 0.000 0.820 NA
#&gt; SRR1927050     1  0.6308      0.752 0.508 0.000 NA
#&gt; SRR1927049     2  0.4291      0.865 0.000 0.820 NA
#&gt; SRR1927047     2  0.1529      0.835 0.000 0.960 NA
#&gt; SRR1927046     1  0.0000      0.789 1.000 0.000 NA
#&gt; SRR1927045     2  0.4291      0.865 0.000 0.820 NA
#&gt; SRR1927044     1  0.0000      0.789 1.000 0.000 NA
#&gt; SRR1927043     2  0.6045      0.830 0.000 0.620 NA
#&gt; SRR1927042     1  0.0000      0.789 1.000 0.000 NA
#&gt; SRR1927040     1  0.0000      0.789 1.000 0.000 NA
#&gt; SRR1927039     2  0.1411      0.835 0.000 0.964 NA
#&gt; SRR1927038     1  0.0000      0.789 1.000 0.000 NA
#&gt; SRR1927037     2  0.3816      0.866 0.000 0.852 NA
#&gt; SRR1927036     1  0.0000      0.789 1.000 0.000 NA
#&gt; SRR1927035     2  0.4121      0.866 0.000 0.832 NA
#&gt; SRR1927034     1  0.6308      0.752 0.508 0.000 NA
#&gt; SRR1927033     2  0.6095      0.828 0.000 0.608 NA
#&gt; SRR1927032     1  0.0000      0.789 1.000 0.000 NA
#&gt; SRR1927031     2  0.1411      0.835 0.000 0.964 NA
#&gt; SRR1927030     1  0.0000      0.789 1.000 0.000 NA
#&gt; SRR1927028     1  0.6308      0.752 0.508 0.000 NA
#&gt; SRR1927029     2  0.6045      0.830 0.000 0.620 NA
#&gt; SRR1927027     2  0.6215      0.651 0.000 0.572 NA
#&gt; SRR1927026     1  0.6308      0.752 0.508 0.000 NA
#&gt; SRR1927024     1  0.6308      0.752 0.508 0.000 NA
#&gt; SRR1927025     2  0.5016      0.782 0.000 0.760 NA
#&gt; SRR1927023     2  0.5016      0.782 0.000 0.760 NA
#&gt; SRR1927022     1  0.5497      0.767 0.708 0.000 NA
#&gt; SRR1927021     2  0.0237      0.845 0.000 0.996 NA
#&gt; SRR1927020     1  0.6308      0.752 0.508 0.000 NA
#&gt; SRR1927019     2  0.4291      0.865 0.000 0.820 NA
#&gt; SRR1927071     1  0.6308      0.752 0.508 0.000 NA
#&gt; SRR1927069     2  0.0424      0.844 0.000 0.992 NA
#&gt; SRR1927070     1  0.0000      0.789 1.000 0.000 NA
#&gt; SRR1927068     1  0.6308      0.752 0.508 0.000 NA
#&gt; SRR1927066     1  0.6308      0.752 0.508 0.000 NA
#&gt; SRR1927065     2  0.6079      0.828 0.000 0.612 NA
#&gt; SRR1927067     2  0.6079      0.828 0.000 0.612 NA
#&gt; SRR1927064     1  0.0000      0.789 1.000 0.000 NA
#&gt; SRR1927063     2  0.4346      0.865 0.000 0.816 NA
#&gt; SRR1927062     1  0.6308      0.752 0.508 0.000 NA
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-2-a').click(function(){
  $('#tab-CV-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-3'>
<p><a id='tab-CV-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1927048     1  0.3975      0.733 0.760 0.000 0.240 0.000
#&gt; SRR1927061     2  0.3356      0.405 0.000 0.824 0.000 0.176
#&gt; SRR1927060     1  0.0336      0.911 0.992 0.000 0.008 0.000
#&gt; SRR1927059     3  0.4972      0.478 0.000 0.456 0.544 0.000
#&gt; SRR1927058     1  0.0000      0.911 1.000 0.000 0.000 0.000
#&gt; SRR1927057     2  0.5864      0.354 0.000 0.664 0.264 0.072
#&gt; SRR1927055     2  0.3681      0.400 0.000 0.816 0.008 0.176
#&gt; SRR1927056     4  0.4464      0.965 0.208 0.000 0.024 0.768
#&gt; SRR1927054     1  0.0336      0.911 0.992 0.000 0.008 0.000
#&gt; SRR1927052     4  0.3908      0.962 0.212 0.000 0.004 0.784
#&gt; SRR1927053     3  0.4972      0.478 0.000 0.456 0.544 0.000
#&gt; SRR1927051     2  0.4103      0.388 0.000 0.744 0.256 0.000
#&gt; SRR1927050     4  0.4562      0.965 0.208 0.000 0.028 0.764
#&gt; SRR1927049     2  0.4103      0.388 0.000 0.744 0.256 0.000
#&gt; SRR1927047     2  0.4992     -0.373 0.000 0.524 0.476 0.000
#&gt; SRR1927046     1  0.3975      0.733 0.760 0.000 0.240 0.000
#&gt; SRR1927045     2  0.4040      0.393 0.000 0.752 0.248 0.000
#&gt; SRR1927044     1  0.0592      0.910 0.984 0.000 0.016 0.000
#&gt; SRR1927043     2  0.3356      0.405 0.000 0.824 0.000 0.176
#&gt; SRR1927042     1  0.0000      0.911 1.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0336      0.911 0.992 0.000 0.008 0.000
#&gt; SRR1927039     3  0.4972      0.478 0.000 0.456 0.544 0.000
#&gt; SRR1927038     1  0.0336      0.911 0.992 0.000 0.008 0.000
#&gt; SRR1927037     2  0.4304      0.334 0.000 0.716 0.284 0.000
#&gt; SRR1927036     1  0.0592      0.910 0.984 0.000 0.016 0.000
#&gt; SRR1927035     2  0.4222      0.363 0.000 0.728 0.272 0.000
#&gt; SRR1927034     4  0.4562      0.965 0.208 0.000 0.028 0.764
#&gt; SRR1927033     2  0.3808      0.401 0.000 0.812 0.012 0.176
#&gt; SRR1927032     1  0.0000      0.911 1.000 0.000 0.000 0.000
#&gt; SRR1927031     3  0.4972      0.478 0.000 0.456 0.544 0.000
#&gt; SRR1927030     1  0.0592      0.910 0.984 0.000 0.016 0.000
#&gt; SRR1927028     4  0.3688      0.965 0.208 0.000 0.000 0.792
#&gt; SRR1927029     2  0.3356      0.405 0.000 0.824 0.000 0.176
#&gt; SRR1927027     3  0.6395      0.278 0.000 0.464 0.472 0.064
#&gt; SRR1927026     4  0.3870      0.964 0.208 0.000 0.004 0.788
#&gt; SRR1927024     4  0.7091      0.728 0.208 0.000 0.224 0.568
#&gt; SRR1927025     3  0.5756      0.460 0.000 0.400 0.568 0.032
#&gt; SRR1927023     3  0.5756      0.460 0.000 0.400 0.568 0.032
#&gt; SRR1927022     1  0.7774     -0.340 0.388 0.000 0.240 0.372
#&gt; SRR1927021     2  0.4955     -0.261 0.000 0.556 0.444 0.000
#&gt; SRR1927020     4  0.4464      0.965 0.208 0.000 0.024 0.768
#&gt; SRR1927019     2  0.4103      0.388 0.000 0.744 0.256 0.000
#&gt; SRR1927071     4  0.3688      0.965 0.208 0.000 0.000 0.792
#&gt; SRR1927069     2  0.4955     -0.261 0.000 0.556 0.444 0.000
#&gt; SRR1927070     1  0.0469      0.910 0.988 0.000 0.012 0.000
#&gt; SRR1927068     4  0.4464      0.965 0.208 0.000 0.024 0.768
#&gt; SRR1927066     4  0.3870      0.964 0.208 0.000 0.004 0.788
#&gt; SRR1927065     2  0.3681      0.400 0.000 0.816 0.008 0.176
#&gt; SRR1927067     2  0.3681      0.400 0.000 0.816 0.008 0.176
#&gt; SRR1927064     1  0.0707      0.909 0.980 0.000 0.020 0.000
#&gt; SRR1927063     2  0.4155      0.396 0.000 0.756 0.240 0.004
#&gt; SRR1927062     4  0.4361      0.966 0.208 0.000 0.020 0.772
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-3-a').click(function(){
  $('#tab-CV-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-4'>
<p><a id='tab-CV-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1927048     1  0.4561     0.3762 0.504 0.000 0.008 0.000 0.488
#&gt; SRR1927061     3  0.3586     0.9899 0.000 0.264 0.736 0.000 0.000
#&gt; SRR1927060     1  0.1764     0.8782 0.928 0.000 0.064 0.000 0.008
#&gt; SRR1927059     2  0.4070     0.6707 0.000 0.804 0.008 0.076 0.112
#&gt; SRR1927058     1  0.0510     0.8879 0.984 0.000 0.016 0.000 0.000
#&gt; SRR1927057     2  0.5963     0.5181 0.000 0.616 0.276 0.076 0.032
#&gt; SRR1927055     3  0.3741     0.9896 0.000 0.264 0.732 0.004 0.000
#&gt; SRR1927056     4  0.2462     0.9654 0.112 0.000 0.000 0.880 0.008
#&gt; SRR1927054     1  0.1764     0.8782 0.928 0.000 0.064 0.000 0.008
#&gt; SRR1927052     4  0.4136     0.9280 0.132 0.000 0.052 0.800 0.016
#&gt; SRR1927053     2  0.4070     0.6707 0.000 0.804 0.008 0.076 0.112
#&gt; SRR1927051     2  0.2852     0.7160 0.000 0.828 0.172 0.000 0.000
#&gt; SRR1927050     4  0.2621     0.9643 0.112 0.000 0.004 0.876 0.008
#&gt; SRR1927049     2  0.3492     0.6919 0.000 0.796 0.188 0.016 0.000
#&gt; SRR1927047     2  0.0854     0.7311 0.000 0.976 0.004 0.012 0.008
#&gt; SRR1927046     1  0.4561     0.3762 0.504 0.000 0.008 0.000 0.488
#&gt; SRR1927045     2  0.3897     0.6744 0.000 0.768 0.204 0.028 0.000
#&gt; SRR1927044     1  0.1012     0.8849 0.968 0.000 0.020 0.000 0.012
#&gt; SRR1927043     3  0.3586     0.9899 0.000 0.264 0.736 0.000 0.000
#&gt; SRR1927042     1  0.0000     0.8881 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.1764     0.8782 0.928 0.000 0.064 0.000 0.008
#&gt; SRR1927039     2  0.4070     0.6707 0.000 0.804 0.008 0.076 0.112
#&gt; SRR1927038     1  0.1764     0.8782 0.928 0.000 0.064 0.000 0.008
#&gt; SRR1927037     2  0.4733     0.7213 0.000 0.768 0.128 0.076 0.028
#&gt; SRR1927036     1  0.1493     0.8757 0.948 0.000 0.028 0.000 0.024
#&gt; SRR1927035     2  0.2605     0.7295 0.000 0.852 0.148 0.000 0.000
#&gt; SRR1927034     4  0.2621     0.9643 0.112 0.000 0.004 0.876 0.008
#&gt; SRR1927033     3  0.4181     0.9541 0.000 0.268 0.712 0.020 0.000
#&gt; SRR1927032     1  0.0290     0.8882 0.992 0.000 0.008 0.000 0.000
#&gt; SRR1927031     2  0.4070     0.6707 0.000 0.804 0.008 0.076 0.112
#&gt; SRR1927030     1  0.1106     0.8858 0.964 0.000 0.024 0.000 0.012
#&gt; SRR1927028     4  0.2835     0.9631 0.112 0.000 0.016 0.868 0.004
#&gt; SRR1927029     3  0.3586     0.9899 0.000 0.264 0.736 0.000 0.000
#&gt; SRR1927027     5  0.7221     0.3251 0.000 0.236 0.272 0.032 0.460
#&gt; SRR1927026     4  0.2621     0.9643 0.112 0.000 0.008 0.876 0.004
#&gt; SRR1927024     5  0.6495    -0.3029 0.112 0.000 0.020 0.400 0.468
#&gt; SRR1927025     5  0.6454     0.3520 0.000 0.304 0.208 0.000 0.488
#&gt; SRR1927023     5  0.6454     0.3520 0.000 0.304 0.208 0.000 0.488
#&gt; SRR1927022     5  0.7074    -0.0589 0.256 0.000 0.024 0.248 0.472
#&gt; SRR1927021     2  0.2142     0.7417 0.000 0.920 0.048 0.028 0.004
#&gt; SRR1927020     4  0.2462     0.9654 0.112 0.000 0.000 0.880 0.008
#&gt; SRR1927019     2  0.2852     0.7160 0.000 0.828 0.172 0.000 0.000
#&gt; SRR1927071     4  0.3609     0.9529 0.112 0.000 0.036 0.836 0.016
#&gt; SRR1927069     2  0.1168     0.7470 0.000 0.960 0.032 0.008 0.000
#&gt; SRR1927070     1  0.1012     0.8849 0.968 0.000 0.020 0.000 0.012
#&gt; SRR1927068     4  0.2462     0.9654 0.112 0.000 0.000 0.880 0.008
#&gt; SRR1927066     4  0.3809     0.9472 0.116 0.000 0.044 0.824 0.016
#&gt; SRR1927065     3  0.3741     0.9896 0.000 0.264 0.732 0.004 0.000
#&gt; SRR1927067     3  0.3741     0.9896 0.000 0.264 0.732 0.004 0.000
#&gt; SRR1927064     1  0.1251     0.8844 0.956 0.000 0.008 0.000 0.036
#&gt; SRR1927063     2  0.3852     0.6440 0.000 0.760 0.220 0.020 0.000
#&gt; SRR1927062     4  0.3729     0.9445 0.124 0.000 0.040 0.824 0.012
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-4-a').click(function(){
  $('#tab-CV-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-5'>
<p><a id='tab-CV-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1927048     6  0.6047      0.602 0.260 0.000 0.040 0.076 0.028 0.596
#&gt; SRR1927061     3  0.3373      0.964 0.000 0.248 0.744 0.000 0.000 0.008
#&gt; SRR1927060     1  0.4568      0.830 0.772 0.000 0.096 0.076 0.036 0.020
#&gt; SRR1927059     2  0.5945      0.460 0.000 0.492 0.004 0.000 0.240 0.264
#&gt; SRR1927058     1  0.2277      0.872 0.892 0.000 0.032 0.076 0.000 0.000
#&gt; SRR1927057     2  0.6185      0.391 0.004 0.524 0.200 0.000 0.020 0.252
#&gt; SRR1927055     3  0.3535      0.960 0.012 0.220 0.760 0.000 0.000 0.008
#&gt; SRR1927056     4  0.0146      0.932 0.000 0.000 0.000 0.996 0.004 0.000
#&gt; SRR1927054     1  0.4588      0.830 0.772 0.000 0.092 0.076 0.040 0.020
#&gt; SRR1927052     4  0.3534      0.867 0.012 0.000 0.052 0.844 0.048 0.044
#&gt; SRR1927053     2  0.5945      0.460 0.000 0.492 0.004 0.000 0.240 0.264
#&gt; SRR1927051     2  0.1265      0.680 0.008 0.948 0.044 0.000 0.000 0.000
#&gt; SRR1927050     4  0.0964      0.926 0.000 0.000 0.016 0.968 0.012 0.004
#&gt; SRR1927049     2  0.1692      0.673 0.008 0.932 0.048 0.000 0.000 0.012
#&gt; SRR1927047     2  0.2981      0.656 0.020 0.848 0.000 0.000 0.116 0.016
#&gt; SRR1927046     6  0.6047      0.602 0.260 0.000 0.040 0.076 0.028 0.596
#&gt; SRR1927045     2  0.2058      0.669 0.024 0.916 0.048 0.000 0.000 0.012
#&gt; SRR1927044     1  0.3562      0.856 0.840 0.000 0.032 0.076 0.036 0.016
#&gt; SRR1927043     3  0.3126      0.968 0.000 0.248 0.752 0.000 0.000 0.000
#&gt; SRR1927042     1  0.1858      0.874 0.912 0.000 0.000 0.076 0.012 0.000
#&gt; SRR1927040     1  0.4568      0.830 0.772 0.000 0.096 0.076 0.036 0.020
#&gt; SRR1927039     2  0.5960      0.454 0.000 0.488 0.004 0.000 0.244 0.264
#&gt; SRR1927038     1  0.4568      0.830 0.772 0.000 0.096 0.076 0.036 0.020
#&gt; SRR1927037     2  0.4358      0.608 0.000 0.680 0.012 0.000 0.032 0.276
#&gt; SRR1927036     1  0.3812      0.845 0.824 0.000 0.056 0.076 0.028 0.016
#&gt; SRR1927035     2  0.0632      0.690 0.000 0.976 0.024 0.000 0.000 0.000
#&gt; SRR1927034     4  0.0964      0.926 0.000 0.000 0.016 0.968 0.012 0.004
#&gt; SRR1927033     3  0.4338      0.940 0.040 0.248 0.700 0.000 0.000 0.012
#&gt; SRR1927032     1  0.2294      0.872 0.896 0.000 0.008 0.076 0.020 0.000
#&gt; SRR1927031     2  0.5960      0.454 0.000 0.488 0.004 0.000 0.244 0.264
#&gt; SRR1927030     1  0.3703      0.860 0.832 0.000 0.040 0.076 0.036 0.016
#&gt; SRR1927028     4  0.1624      0.926 0.000 0.000 0.004 0.936 0.020 0.040
#&gt; SRR1927029     3  0.3126      0.968 0.000 0.248 0.752 0.000 0.000 0.000
#&gt; SRR1927027     5  0.4311      0.886 0.004 0.068 0.120 0.012 0.780 0.016
#&gt; SRR1927026     4  0.1820      0.924 0.000 0.000 0.016 0.928 0.012 0.044
#&gt; SRR1927024     6  0.3878      0.451 0.000 0.000 0.004 0.348 0.004 0.644
#&gt; SRR1927025     5  0.3032      0.943 0.000 0.104 0.056 0.000 0.840 0.000
#&gt; SRR1927023     5  0.3032      0.943 0.000 0.104 0.056 0.000 0.840 0.000
#&gt; SRR1927022     6  0.5572      0.648 0.092 0.000 0.008 0.248 0.028 0.624
#&gt; SRR1927021     2  0.3128      0.663 0.032 0.848 0.004 0.000 0.104 0.012
#&gt; SRR1927020     4  0.0508      0.931 0.000 0.000 0.004 0.984 0.012 0.000
#&gt; SRR1927019     2  0.1590      0.676 0.008 0.936 0.048 0.000 0.000 0.008
#&gt; SRR1927071     4  0.2411      0.911 0.000 0.000 0.032 0.900 0.024 0.044
#&gt; SRR1927069     2  0.2747      0.669 0.020 0.868 0.000 0.000 0.096 0.016
#&gt; SRR1927070     1  0.3612      0.855 0.836 0.000 0.040 0.076 0.036 0.012
#&gt; SRR1927068     4  0.0146      0.932 0.000 0.000 0.000 0.996 0.004 0.000
#&gt; SRR1927066     4  0.2776      0.902 0.004 0.000 0.044 0.884 0.028 0.040
#&gt; SRR1927065     3  0.3081      0.963 0.000 0.220 0.776 0.000 0.000 0.004
#&gt; SRR1927067     3  0.3329      0.962 0.008 0.220 0.768 0.000 0.000 0.004
#&gt; SRR1927064     1  0.4155      0.821 0.808 0.000 0.044 0.076 0.040 0.032
#&gt; SRR1927063     2  0.2402      0.640 0.008 0.888 0.084 0.000 0.000 0.020
#&gt; SRR1927062     4  0.2039      0.904 0.012 0.000 0.052 0.916 0.020 0.000
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-5-a').click(function(){
  $('#tab-CV-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-CV-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-signatures'>
<ul>
<li><a href='#tab-CV-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-kmeans-signature_compare](figure_cola/CV-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-CV-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-kmeans-collect-classes](figure_cola/CV-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:skmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "skmeans"]
# you can also extract it by
# res = res_list["CV:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16868 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-skmeans-collect-plots](figure_cola/CV-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-skmeans-select-partition-number](figure_cola/CV-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5095 0.491   0.491
#> 3 3 1.000           0.968       0.978         0.2687 0.864   0.724
#> 4 4 0.868           0.848       0.906         0.1565 0.897   0.711
#> 5 5 0.871           0.891       0.927         0.0384 0.971   0.884
#> 6 6 0.879           0.874       0.910         0.0433 0.962   0.835
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-classes'>
<ul>
<li><a href='#tab-CV-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-skmeans-get-classes-1'>
<p><a id='tab-CV-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1927048     1       0          1  1  0
#&gt; SRR1927061     2       0          1  0  1
#&gt; SRR1927060     1       0          1  1  0
#&gt; SRR1927059     2       0          1  0  1
#&gt; SRR1927058     1       0          1  1  0
#&gt; SRR1927057     2       0          1  0  1
#&gt; SRR1927055     2       0          1  0  1
#&gt; SRR1927056     1       0          1  1  0
#&gt; SRR1927054     1       0          1  1  0
#&gt; SRR1927052     1       0          1  1  0
#&gt; SRR1927053     2       0          1  0  1
#&gt; SRR1927051     2       0          1  0  1
#&gt; SRR1927050     1       0          1  1  0
#&gt; SRR1927049     2       0          1  0  1
#&gt; SRR1927047     2       0          1  0  1
#&gt; SRR1927046     1       0          1  1  0
#&gt; SRR1927045     2       0          1  0  1
#&gt; SRR1927044     1       0          1  1  0
#&gt; SRR1927043     2       0          1  0  1
#&gt; SRR1927042     1       0          1  1  0
#&gt; SRR1927040     1       0          1  1  0
#&gt; SRR1927039     2       0          1  0  1
#&gt; SRR1927038     1       0          1  1  0
#&gt; SRR1927037     2       0          1  0  1
#&gt; SRR1927036     1       0          1  1  0
#&gt; SRR1927035     2       0          1  0  1
#&gt; SRR1927034     1       0          1  1  0
#&gt; SRR1927033     2       0          1  0  1
#&gt; SRR1927032     1       0          1  1  0
#&gt; SRR1927031     2       0          1  0  1
#&gt; SRR1927030     1       0          1  1  0
#&gt; SRR1927028     1       0          1  1  0
#&gt; SRR1927029     2       0          1  0  1
#&gt; SRR1927027     2       0          1  0  1
#&gt; SRR1927026     1       0          1  1  0
#&gt; SRR1927024     1       0          1  1  0
#&gt; SRR1927025     2       0          1  0  1
#&gt; SRR1927023     2       0          1  0  1
#&gt; SRR1927022     1       0          1  1  0
#&gt; SRR1927021     2       0          1  0  1
#&gt; SRR1927020     1       0          1  1  0
#&gt; SRR1927019     2       0          1  0  1
#&gt; SRR1927071     1       0          1  1  0
#&gt; SRR1927069     2       0          1  0  1
#&gt; SRR1927070     1       0          1  1  0
#&gt; SRR1927068     1       0          1  1  0
#&gt; SRR1927066     1       0          1  1  0
#&gt; SRR1927065     2       0          1  0  1
#&gt; SRR1927067     2       0          1  0  1
#&gt; SRR1927064     1       0          1  1  0
#&gt; SRR1927063     2       0          1  0  1
#&gt; SRR1927062     1       0          1  1  0
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-1-a').click(function(){
  $('#tab-CV-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-2'>
<p><a id='tab-CV-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1927048     1  0.0000      0.973 1.000 0.000 0.000
#&gt; SRR1927061     2  0.0592      0.982 0.000 0.988 0.012
#&gt; SRR1927060     1  0.0000      0.973 1.000 0.000 0.000
#&gt; SRR1927059     2  0.0747      0.981 0.000 0.984 0.016
#&gt; SRR1927058     1  0.0000      0.973 1.000 0.000 0.000
#&gt; SRR1927057     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1927055     2  0.0592      0.982 0.000 0.988 0.012
#&gt; SRR1927056     3  0.1163      0.998 0.028 0.000 0.972
#&gt; SRR1927054     1  0.0000      0.973 1.000 0.000 0.000
#&gt; SRR1927052     3  0.1163      0.998 0.028 0.000 0.972
#&gt; SRR1927053     2  0.0747      0.981 0.000 0.984 0.016
#&gt; SRR1927051     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1927050     3  0.1163      0.998 0.028 0.000 0.972
#&gt; SRR1927049     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1927047     2  0.0747      0.981 0.000 0.984 0.016
#&gt; SRR1927046     1  0.0000      0.973 1.000 0.000 0.000
#&gt; SRR1927045     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1927044     1  0.0000      0.973 1.000 0.000 0.000
#&gt; SRR1927043     2  0.0592      0.982 0.000 0.988 0.012
#&gt; SRR1927042     1  0.0000      0.973 1.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      0.973 1.000 0.000 0.000
#&gt; SRR1927039     2  0.0747      0.981 0.000 0.984 0.016
#&gt; SRR1927038     1  0.0000      0.973 1.000 0.000 0.000
#&gt; SRR1927037     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1927036     1  0.0000      0.973 1.000 0.000 0.000
#&gt; SRR1927035     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1927034     3  0.1163      0.998 0.028 0.000 0.972
#&gt; SRR1927033     2  0.0592      0.982 0.000 0.988 0.012
#&gt; SRR1927032     1  0.0000      0.973 1.000 0.000 0.000
#&gt; SRR1927031     2  0.0747      0.981 0.000 0.984 0.016
#&gt; SRR1927030     1  0.0000      0.973 1.000 0.000 0.000
#&gt; SRR1927028     3  0.1163      0.998 0.028 0.000 0.972
#&gt; SRR1927029     2  0.0592      0.982 0.000 0.988 0.012
#&gt; SRR1927027     2  0.4842      0.744 0.000 0.776 0.224
#&gt; SRR1927026     3  0.1163      0.998 0.028 0.000 0.972
#&gt; SRR1927024     3  0.1860      0.974 0.052 0.000 0.948
#&gt; SRR1927025     2  0.0892      0.981 0.000 0.980 0.020
#&gt; SRR1927023     2  0.0892      0.981 0.000 0.980 0.020
#&gt; SRR1927022     1  0.5926      0.416 0.644 0.000 0.356
#&gt; SRR1927021     2  0.0592      0.982 0.000 0.988 0.012
#&gt; SRR1927020     3  0.1163      0.998 0.028 0.000 0.972
#&gt; SRR1927019     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1927071     3  0.1163      0.998 0.028 0.000 0.972
#&gt; SRR1927069     2  0.0592      0.982 0.000 0.988 0.012
#&gt; SRR1927070     1  0.0000      0.973 1.000 0.000 0.000
#&gt; SRR1927068     3  0.1163      0.998 0.028 0.000 0.972
#&gt; SRR1927066     3  0.1163      0.998 0.028 0.000 0.972
#&gt; SRR1927065     2  0.0592      0.982 0.000 0.988 0.012
#&gt; SRR1927067     2  0.0592      0.982 0.000 0.988 0.012
#&gt; SRR1927064     1  0.0000      0.973 1.000 0.000 0.000
#&gt; SRR1927063     2  0.0000      0.984 0.000 1.000 0.000
#&gt; SRR1927062     3  0.1163      0.998 0.028 0.000 0.972
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-2-a').click(function(){
  $('#tab-CV-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-3'>
<p><a id='tab-CV-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1927048     1  0.0000      0.967 1.000 0.000 0.000 0.000
#&gt; SRR1927061     3  0.1637      0.914 0.000 0.060 0.940 0.000
#&gt; SRR1927060     1  0.0188      0.968 0.996 0.000 0.000 0.004
#&gt; SRR1927059     2  0.0188      0.717 0.000 0.996 0.004 0.000
#&gt; SRR1927058     1  0.0188      0.968 0.996 0.000 0.000 0.004
#&gt; SRR1927057     2  0.4817      0.630 0.000 0.612 0.388 0.000
#&gt; SRR1927055     3  0.1557      0.913 0.000 0.056 0.944 0.000
#&gt; SRR1927056     4  0.0336      0.995 0.008 0.000 0.000 0.992
#&gt; SRR1927054     1  0.0000      0.967 1.000 0.000 0.000 0.000
#&gt; SRR1927052     4  0.0592      0.988 0.016 0.000 0.000 0.984
#&gt; SRR1927053     2  0.0188      0.717 0.000 0.996 0.004 0.000
#&gt; SRR1927051     2  0.4713      0.669 0.000 0.640 0.360 0.000
#&gt; SRR1927050     4  0.0336      0.995 0.008 0.000 0.000 0.992
#&gt; SRR1927049     2  0.4713      0.669 0.000 0.640 0.360 0.000
#&gt; SRR1927047     2  0.0592      0.720 0.000 0.984 0.016 0.000
#&gt; SRR1927046     1  0.0000      0.967 1.000 0.000 0.000 0.000
#&gt; SRR1927045     2  0.4713      0.669 0.000 0.640 0.360 0.000
#&gt; SRR1927044     1  0.0188      0.968 0.996 0.000 0.000 0.004
#&gt; SRR1927043     3  0.1637      0.914 0.000 0.060 0.940 0.000
#&gt; SRR1927042     1  0.0188      0.968 0.996 0.000 0.000 0.004
#&gt; SRR1927040     1  0.0188      0.968 0.996 0.000 0.000 0.004
#&gt; SRR1927039     2  0.0000      0.715 0.000 1.000 0.000 0.000
#&gt; SRR1927038     1  0.0188      0.968 0.996 0.000 0.000 0.004
#&gt; SRR1927037     2  0.4605      0.683 0.000 0.664 0.336 0.000
#&gt; SRR1927036     1  0.0188      0.968 0.996 0.000 0.000 0.004
#&gt; SRR1927035     2  0.4624      0.681 0.000 0.660 0.340 0.000
#&gt; SRR1927034     4  0.0336      0.995 0.008 0.000 0.000 0.992
#&gt; SRR1927033     3  0.1557      0.913 0.000 0.056 0.944 0.000
#&gt; SRR1927032     1  0.0188      0.968 0.996 0.000 0.000 0.004
#&gt; SRR1927031     2  0.0000      0.715 0.000 1.000 0.000 0.000
#&gt; SRR1927030     1  0.0188      0.968 0.996 0.000 0.000 0.004
#&gt; SRR1927028     4  0.0336      0.995 0.008 0.000 0.000 0.992
#&gt; SRR1927029     3  0.1637      0.914 0.000 0.060 0.940 0.000
#&gt; SRR1927027     3  0.4990      0.374 0.000 0.352 0.640 0.008
#&gt; SRR1927026     4  0.0336      0.995 0.008 0.000 0.000 0.992
#&gt; SRR1927024     4  0.1389      0.957 0.048 0.000 0.000 0.952
#&gt; SRR1927025     2  0.3257      0.594 0.000 0.844 0.152 0.004
#&gt; SRR1927023     2  0.3401      0.591 0.000 0.840 0.152 0.008
#&gt; SRR1927022     1  0.4817      0.348 0.612 0.000 0.000 0.388
#&gt; SRR1927021     2  0.2760      0.729 0.000 0.872 0.128 0.000
#&gt; SRR1927020     4  0.0336      0.995 0.008 0.000 0.000 0.992
#&gt; SRR1927019     2  0.4713      0.669 0.000 0.640 0.360 0.000
#&gt; SRR1927071     4  0.0336      0.995 0.008 0.000 0.000 0.992
#&gt; SRR1927069     2  0.2345      0.730 0.000 0.900 0.100 0.000
#&gt; SRR1927070     1  0.0188      0.968 0.996 0.000 0.000 0.004
#&gt; SRR1927068     4  0.0336      0.995 0.008 0.000 0.000 0.992
#&gt; SRR1927066     4  0.0336      0.995 0.008 0.000 0.000 0.992
#&gt; SRR1927065     3  0.1637      0.914 0.000 0.060 0.940 0.000
#&gt; SRR1927067     3  0.1557      0.913 0.000 0.056 0.944 0.000
#&gt; SRR1927064     1  0.0000      0.967 1.000 0.000 0.000 0.000
#&gt; SRR1927063     2  0.4761      0.654 0.000 0.628 0.372 0.000
#&gt; SRR1927062     4  0.0336      0.995 0.008 0.000 0.000 0.992
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-3-a').click(function(){
  $('#tab-CV-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-4'>
<p><a id='tab-CV-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1927048     1  0.3146      0.822 0.844 0.000 0.028 0.000 0.128
#&gt; SRR1927061     3  0.0794      1.000 0.000 0.028 0.972 0.000 0.000
#&gt; SRR1927060     1  0.0000      0.938 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.0510      0.821 0.000 0.984 0.000 0.000 0.016
#&gt; SRR1927058     1  0.0000      0.938 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927057     2  0.4063      0.749 0.000 0.708 0.280 0.000 0.012
#&gt; SRR1927055     3  0.0794      1.000 0.000 0.028 0.972 0.000 0.000
#&gt; SRR1927056     4  0.0162      0.976 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1927054     1  0.0000      0.938 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927052     4  0.0404      0.966 0.012 0.000 0.000 0.988 0.000
#&gt; SRR1927053     2  0.0404      0.823 0.000 0.988 0.000 0.000 0.012
#&gt; SRR1927051     2  0.3143      0.827 0.000 0.796 0.204 0.000 0.000
#&gt; SRR1927050     4  0.0162      0.976 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1927049     2  0.3274      0.819 0.000 0.780 0.220 0.000 0.000
#&gt; SRR1927047     2  0.0162      0.827 0.000 0.996 0.004 0.000 0.000
#&gt; SRR1927046     1  0.3146      0.822 0.844 0.000 0.028 0.000 0.128
#&gt; SRR1927045     2  0.3707      0.759 0.000 0.716 0.284 0.000 0.000
#&gt; SRR1927044     1  0.0000      0.938 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927043     3  0.0794      1.000 0.000 0.028 0.972 0.000 0.000
#&gt; SRR1927042     1  0.0000      0.938 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      0.938 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927039     2  0.0510      0.821 0.000 0.984 0.000 0.000 0.016
#&gt; SRR1927038     1  0.0000      0.938 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.2249      0.849 0.000 0.896 0.096 0.000 0.008
#&gt; SRR1927036     1  0.0000      0.938 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927035     2  0.2516      0.845 0.000 0.860 0.140 0.000 0.000
#&gt; SRR1927034     4  0.0162      0.976 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1927033     3  0.0794      1.000 0.000 0.028 0.972 0.000 0.000
#&gt; SRR1927032     1  0.0000      0.938 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927031     2  0.0510      0.821 0.000 0.984 0.000 0.000 0.016
#&gt; SRR1927030     1  0.0000      0.938 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927028     4  0.0000      0.976 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927029     3  0.0794      1.000 0.000 0.028 0.972 0.000 0.000
#&gt; SRR1927027     5  0.3242      0.843 0.000 0.076 0.072 0.000 0.852
#&gt; SRR1927026     4  0.0000      0.976 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927024     4  0.4471      0.743 0.056 0.000 0.028 0.784 0.132
#&gt; SRR1927025     5  0.3756      0.842 0.000 0.248 0.008 0.000 0.744
#&gt; SRR1927023     5  0.2719      0.892 0.000 0.144 0.004 0.000 0.852
#&gt; SRR1927022     1  0.6717      0.237 0.488 0.000 0.028 0.356 0.128
#&gt; SRR1927021     2  0.1478      0.846 0.000 0.936 0.064 0.000 0.000
#&gt; SRR1927020     4  0.0162      0.976 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1927019     2  0.3242      0.822 0.000 0.784 0.216 0.000 0.000
#&gt; SRR1927071     4  0.0000      0.976 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927069     2  0.0794      0.838 0.000 0.972 0.028 0.000 0.000
#&gt; SRR1927070     1  0.0000      0.938 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927068     4  0.0162      0.976 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1927066     4  0.0000      0.976 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927065     3  0.0794      1.000 0.000 0.028 0.972 0.000 0.000
#&gt; SRR1927067     3  0.0794      1.000 0.000 0.028 0.972 0.000 0.000
#&gt; SRR1927064     1  0.0290      0.933 0.992 0.000 0.000 0.000 0.008
#&gt; SRR1927063     2  0.3983      0.678 0.000 0.660 0.340 0.000 0.000
#&gt; SRR1927062     4  0.0162      0.974 0.004 0.000 0.000 0.996 0.000
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-4-a').click(function(){
  $('#tab-CV-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-5'>
<p><a id='tab-CV-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1927048     6  0.3531      0.706 0.328 0.000 0.000 0.000 0.000 0.672
#&gt; SRR1927061     3  0.0000      0.998 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927060     1  0.0000      0.998 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.3337      0.706 0.000 0.736 0.000 0.000 0.260 0.004
#&gt; SRR1927058     1  0.0000      0.998 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927057     2  0.5685      0.602 0.000 0.528 0.240 0.000 0.232 0.000
#&gt; SRR1927055     3  0.0000      0.998 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927056     4  0.0000      0.981 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927054     1  0.0000      0.998 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927052     4  0.1867      0.903 0.064 0.000 0.000 0.916 0.000 0.020
#&gt; SRR1927053     2  0.3337      0.706 0.000 0.736 0.000 0.000 0.260 0.004
#&gt; SRR1927051     2  0.2260      0.751 0.000 0.860 0.140 0.000 0.000 0.000
#&gt; SRR1927050     4  0.0000      0.981 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927049     2  0.2631      0.732 0.000 0.820 0.180 0.000 0.000 0.000
#&gt; SRR1927047     2  0.0653      0.758 0.000 0.980 0.004 0.000 0.012 0.004
#&gt; SRR1927046     6  0.3428      0.721 0.304 0.000 0.000 0.000 0.000 0.696
#&gt; SRR1927045     2  0.3151      0.673 0.000 0.748 0.252 0.000 0.000 0.000
#&gt; SRR1927044     1  0.0000      0.998 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927043     3  0.0000      0.998 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927042     1  0.0000      0.998 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      0.998 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927039     2  0.3337      0.706 0.000 0.736 0.000 0.000 0.260 0.004
#&gt; SRR1927038     1  0.0000      0.998 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.3780      0.712 0.000 0.728 0.020 0.000 0.248 0.004
#&gt; SRR1927036     1  0.0000      0.998 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927035     2  0.1663      0.762 0.000 0.912 0.088 0.000 0.000 0.000
#&gt; SRR1927034     4  0.0000      0.981 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927033     3  0.0260      0.989 0.000 0.008 0.992 0.000 0.000 0.000
#&gt; SRR1927032     1  0.0000      0.998 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927031     2  0.3337      0.706 0.000 0.736 0.000 0.000 0.260 0.004
#&gt; SRR1927030     1  0.0000      0.998 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927028     4  0.0146      0.980 0.000 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1927029     3  0.0000      0.998 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927027     5  0.3360      0.868 0.000 0.000 0.004 0.000 0.732 0.264
#&gt; SRR1927026     4  0.0458      0.975 0.000 0.000 0.000 0.984 0.000 0.016
#&gt; SRR1927024     6  0.3695      0.535 0.024 0.000 0.000 0.244 0.000 0.732
#&gt; SRR1927025     5  0.5113      0.786 0.000 0.168 0.000 0.000 0.628 0.204
#&gt; SRR1927023     5  0.3534      0.881 0.000 0.016 0.000 0.000 0.740 0.244
#&gt; SRR1927022     6  0.4421      0.706 0.156 0.000 0.000 0.128 0.000 0.716
#&gt; SRR1927021     2  0.1225      0.760 0.000 0.952 0.036 0.000 0.012 0.000
#&gt; SRR1927020     4  0.0000      0.981 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927019     2  0.2632      0.743 0.000 0.832 0.164 0.000 0.004 0.000
#&gt; SRR1927071     4  0.0547      0.973 0.000 0.000 0.000 0.980 0.000 0.020
#&gt; SRR1927069     2  0.0405      0.759 0.000 0.988 0.004 0.000 0.008 0.000
#&gt; SRR1927070     1  0.0000      0.998 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927068     4  0.0000      0.981 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927066     4  0.0260      0.979 0.000 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1927065     3  0.0000      0.998 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927067     3  0.0000      0.998 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927064     1  0.0547      0.974 0.980 0.000 0.000 0.000 0.000 0.020
#&gt; SRR1927063     2  0.3482      0.596 0.000 0.684 0.316 0.000 0.000 0.000
#&gt; SRR1927062     4  0.0865      0.950 0.036 0.000 0.000 0.964 0.000 0.000
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-5-a').click(function(){
  $('#tab-CV-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-CV-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-signatures'>
<ul>
<li><a href='#tab-CV-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-skmeans-signature_compare](figure_cola/CV-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-CV-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-skmeans-collect-classes](figure_cola/CV-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:pam**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "pam"]
# you can also extract it by
# res = res_list["CV:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16868 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-pam-collect-plots](figure_cola/CV-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-pam-select-partition-number](figure_cola/CV-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.991       0.996         0.5091 0.491   0.491
#> 3 3 0.699           0.583       0.794         0.2356 0.905   0.806
#> 4 4 0.704           0.741       0.887         0.2019 0.769   0.466
#> 5 5 0.748           0.680       0.809         0.0451 0.919   0.690
#> 6 6 0.816           0.762       0.815         0.0343 0.934   0.711
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-classes'>
<ul>
<li><a href='#tab-CV-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-pam-get-classes-1'>
<p><a id='tab-CV-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1927048     1    0.00      1.000 1.000 0.000
#&gt; SRR1927061     2    0.00      0.991 0.000 1.000
#&gt; SRR1927060     1    0.00      1.000 1.000 0.000
#&gt; SRR1927059     2    0.00      0.991 0.000 1.000
#&gt; SRR1927058     1    0.00      1.000 1.000 0.000
#&gt; SRR1927057     2    0.00      0.991 0.000 1.000
#&gt; SRR1927055     2    0.00      0.991 0.000 1.000
#&gt; SRR1927056     1    0.00      1.000 1.000 0.000
#&gt; SRR1927054     1    0.00      1.000 1.000 0.000
#&gt; SRR1927052     1    0.00      1.000 1.000 0.000
#&gt; SRR1927053     2    0.00      0.991 0.000 1.000
#&gt; SRR1927051     2    0.00      0.991 0.000 1.000
#&gt; SRR1927050     1    0.00      1.000 1.000 0.000
#&gt; SRR1927049     2    0.00      0.991 0.000 1.000
#&gt; SRR1927047     2    0.00      0.991 0.000 1.000
#&gt; SRR1927046     1    0.00      1.000 1.000 0.000
#&gt; SRR1927045     2    0.00      0.991 0.000 1.000
#&gt; SRR1927044     1    0.00      1.000 1.000 0.000
#&gt; SRR1927043     2    0.00      0.991 0.000 1.000
#&gt; SRR1927042     1    0.00      1.000 1.000 0.000
#&gt; SRR1927040     1    0.00      1.000 1.000 0.000
#&gt; SRR1927039     2    0.00      0.991 0.000 1.000
#&gt; SRR1927038     1    0.00      1.000 1.000 0.000
#&gt; SRR1927037     2    0.00      0.991 0.000 1.000
#&gt; SRR1927036     1    0.00      1.000 1.000 0.000
#&gt; SRR1927035     2    0.00      0.991 0.000 1.000
#&gt; SRR1927034     1    0.00      1.000 1.000 0.000
#&gt; SRR1927033     2    0.00      0.991 0.000 1.000
#&gt; SRR1927032     1    0.00      1.000 1.000 0.000
#&gt; SRR1927031     2    0.00      0.991 0.000 1.000
#&gt; SRR1927030     1    0.00      1.000 1.000 0.000
#&gt; SRR1927028     1    0.00      1.000 1.000 0.000
#&gt; SRR1927029     2    0.00      0.991 0.000 1.000
#&gt; SRR1927027     2    0.73      0.744 0.204 0.796
#&gt; SRR1927026     1    0.00      1.000 1.000 0.000
#&gt; SRR1927024     1    0.00      1.000 1.000 0.000
#&gt; SRR1927025     2    0.00      0.991 0.000 1.000
#&gt; SRR1927023     2    0.00      0.991 0.000 1.000
#&gt; SRR1927022     1    0.00      1.000 1.000 0.000
#&gt; SRR1927021     2    0.00      0.991 0.000 1.000
#&gt; SRR1927020     1    0.00      1.000 1.000 0.000
#&gt; SRR1927019     2    0.00      0.991 0.000 1.000
#&gt; SRR1927071     1    0.00      1.000 1.000 0.000
#&gt; SRR1927069     2    0.00      0.991 0.000 1.000
#&gt; SRR1927070     1    0.00      1.000 1.000 0.000
#&gt; SRR1927068     1    0.00      1.000 1.000 0.000
#&gt; SRR1927066     1    0.00      1.000 1.000 0.000
#&gt; SRR1927065     2    0.00      0.991 0.000 1.000
#&gt; SRR1927067     2    0.00      0.991 0.000 1.000
#&gt; SRR1927064     1    0.00      1.000 1.000 0.000
#&gt; SRR1927063     2    0.00      0.991 0.000 1.000
#&gt; SRR1927062     1    0.00      1.000 1.000 0.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-1-a').click(function(){
  $('#tab-CV-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-2'>
<p><a id='tab-CV-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1927048     1  0.1643      0.922 0.956 0.000 0.044
#&gt; SRR1927061     2  0.5621      0.501 0.000 0.692 0.308
#&gt; SRR1927060     1  0.1643      0.922 0.956 0.000 0.044
#&gt; SRR1927059     3  0.6308      0.716 0.000 0.492 0.508
#&gt; SRR1927058     1  0.1643      0.922 0.956 0.000 0.044
#&gt; SRR1927057     3  0.6295      0.667 0.000 0.472 0.528
#&gt; SRR1927055     2  0.5621      0.501 0.000 0.692 0.308
#&gt; SRR1927056     1  0.3686      0.915 0.860 0.000 0.140
#&gt; SRR1927054     1  0.1643      0.922 0.956 0.000 0.044
#&gt; SRR1927052     1  0.3267      0.919 0.884 0.000 0.116
#&gt; SRR1927053     3  0.6308      0.716 0.000 0.492 0.508
#&gt; SRR1927051     2  0.5327     -0.346 0.000 0.728 0.272
#&gt; SRR1927050     1  0.3686      0.915 0.860 0.000 0.140
#&gt; SRR1927049     2  0.0424      0.268 0.000 0.992 0.008
#&gt; SRR1927047     2  0.6180     -0.592 0.000 0.584 0.416
#&gt; SRR1927046     1  0.0747      0.925 0.984 0.000 0.016
#&gt; SRR1927045     2  0.5254      0.484 0.000 0.736 0.264
#&gt; SRR1927044     1  0.1529      0.923 0.960 0.000 0.040
#&gt; SRR1927043     2  0.5621      0.501 0.000 0.692 0.308
#&gt; SRR1927042     1  0.1643      0.922 0.956 0.000 0.044
#&gt; SRR1927040     1  0.1643      0.922 0.956 0.000 0.044
#&gt; SRR1927039     3  0.6308      0.716 0.000 0.492 0.508
#&gt; SRR1927038     1  0.1643      0.922 0.956 0.000 0.044
#&gt; SRR1927037     2  0.6215     -0.616 0.000 0.572 0.428
#&gt; SRR1927036     1  0.0000      0.926 1.000 0.000 0.000
#&gt; SRR1927035     2  0.6168     -0.587 0.000 0.588 0.412
#&gt; SRR1927034     1  0.3686      0.915 0.860 0.000 0.140
#&gt; SRR1927033     2  0.5621      0.501 0.000 0.692 0.308
#&gt; SRR1927032     1  0.1643      0.922 0.956 0.000 0.044
#&gt; SRR1927031     3  0.6308      0.716 0.000 0.492 0.508
#&gt; SRR1927030     1  0.1643      0.922 0.956 0.000 0.044
#&gt; SRR1927028     1  0.3686      0.915 0.860 0.000 0.140
#&gt; SRR1927029     2  0.5621      0.501 0.000 0.692 0.308
#&gt; SRR1927027     2  0.6521      0.356 0.004 0.504 0.492
#&gt; SRR1927026     1  0.3686      0.915 0.860 0.000 0.140
#&gt; SRR1927024     1  0.3686      0.915 0.860 0.000 0.140
#&gt; SRR1927025     3  0.6168     -0.240 0.000 0.412 0.588
#&gt; SRR1927023     3  0.5138      0.414 0.000 0.252 0.748
#&gt; SRR1927022     1  0.1860      0.924 0.948 0.000 0.052
#&gt; SRR1927021     2  0.6045     -0.544 0.000 0.620 0.380
#&gt; SRR1927020     1  0.3686      0.915 0.860 0.000 0.140
#&gt; SRR1927019     2  0.1031      0.244 0.000 0.976 0.024
#&gt; SRR1927071     1  0.3619      0.916 0.864 0.000 0.136
#&gt; SRR1927069     2  0.6180     -0.592 0.000 0.584 0.416
#&gt; SRR1927070     1  0.0000      0.926 1.000 0.000 0.000
#&gt; SRR1927068     1  0.3686      0.915 0.860 0.000 0.140
#&gt; SRR1927066     1  0.3686      0.915 0.860 0.000 0.140
#&gt; SRR1927065     2  0.5621      0.501 0.000 0.692 0.308
#&gt; SRR1927067     2  0.6111      0.429 0.000 0.604 0.396
#&gt; SRR1927064     1  0.1643      0.922 0.956 0.000 0.044
#&gt; SRR1927063     2  0.0592      0.263 0.000 0.988 0.012
#&gt; SRR1927062     1  0.3619      0.916 0.864 0.000 0.136
</code></pre>

<script>
$('#tab-CV-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-2-a').click(function(){
  $('#tab-CV-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-3'>
<p><a id='tab-CV-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1927048     1  0.0000      0.860 1.000 0.000 0.000 0.000
#&gt; SRR1927061     3  0.0000      0.786 0.000 0.000 1.000 0.000
#&gt; SRR1927060     1  0.0000      0.860 1.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.0000      0.838 0.000 1.000 0.000 0.000
#&gt; SRR1927058     1  0.0000      0.860 1.000 0.000 0.000 0.000
#&gt; SRR1927057     2  0.2973      0.789 0.000 0.856 0.144 0.000
#&gt; SRR1927055     3  0.0000      0.786 0.000 0.000 1.000 0.000
#&gt; SRR1927056     4  0.0000      0.919 0.000 0.000 0.000 1.000
#&gt; SRR1927054     1  0.0000      0.860 1.000 0.000 0.000 0.000
#&gt; SRR1927052     4  0.4304      0.584 0.284 0.000 0.000 0.716
#&gt; SRR1927053     2  0.0000      0.838 0.000 1.000 0.000 0.000
#&gt; SRR1927051     2  0.4522      0.543 0.000 0.680 0.320 0.000
#&gt; SRR1927050     4  0.0000      0.919 0.000 0.000 0.000 1.000
#&gt; SRR1927049     3  0.4761      0.360 0.000 0.372 0.628 0.000
#&gt; SRR1927047     2  0.2469      0.838 0.000 0.892 0.108 0.000
#&gt; SRR1927046     1  0.2814      0.782 0.868 0.000 0.000 0.132
#&gt; SRR1927045     3  0.1637      0.755 0.000 0.060 0.940 0.000
#&gt; SRR1927044     1  0.1557      0.840 0.944 0.000 0.000 0.056
#&gt; SRR1927043     3  0.0000      0.786 0.000 0.000 1.000 0.000
#&gt; SRR1927042     1  0.0000      0.860 1.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      0.860 1.000 0.000 0.000 0.000
#&gt; SRR1927039     2  0.0000      0.838 0.000 1.000 0.000 0.000
#&gt; SRR1927038     1  0.0000      0.860 1.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.2081      0.844 0.000 0.916 0.084 0.000
#&gt; SRR1927036     1  0.4955      0.265 0.556 0.000 0.000 0.444
#&gt; SRR1927035     2  0.2921      0.820 0.000 0.860 0.140 0.000
#&gt; SRR1927034     4  0.0000      0.919 0.000 0.000 0.000 1.000
#&gt; SRR1927033     3  0.0000      0.786 0.000 0.000 1.000 0.000
#&gt; SRR1927032     1  0.0592      0.857 0.984 0.000 0.000 0.016
#&gt; SRR1927031     2  0.0000      0.838 0.000 1.000 0.000 0.000
#&gt; SRR1927030     1  0.2704      0.790 0.876 0.000 0.000 0.124
#&gt; SRR1927028     4  0.3024      0.822 0.148 0.000 0.000 0.852
#&gt; SRR1927029     3  0.0000      0.786 0.000 0.000 1.000 0.000
#&gt; SRR1927027     3  0.5546      0.545 0.000 0.268 0.680 0.052
#&gt; SRR1927026     4  0.0000      0.919 0.000 0.000 0.000 1.000
#&gt; SRR1927024     4  0.2814      0.837 0.132 0.000 0.000 0.868
#&gt; SRR1927025     3  0.4955      0.251 0.000 0.444 0.556 0.000
#&gt; SRR1927023     2  0.4164      0.486 0.000 0.736 0.264 0.000
#&gt; SRR1927022     1  0.4989      0.172 0.528 0.000 0.000 0.472
#&gt; SRR1927021     2  0.3610      0.753 0.000 0.800 0.200 0.000
#&gt; SRR1927020     4  0.0000      0.919 0.000 0.000 0.000 1.000
#&gt; SRR1927019     3  0.4843      0.301 0.000 0.396 0.604 0.000
#&gt; SRR1927071     4  0.0188      0.918 0.004 0.000 0.000 0.996
#&gt; SRR1927069     2  0.2469      0.838 0.000 0.892 0.108 0.000
#&gt; SRR1927070     1  0.4955      0.265 0.556 0.000 0.000 0.444
#&gt; SRR1927068     4  0.0000      0.919 0.000 0.000 0.000 1.000
#&gt; SRR1927066     4  0.3024      0.822 0.148 0.000 0.000 0.852
#&gt; SRR1927065     3  0.0000      0.786 0.000 0.000 1.000 0.000
#&gt; SRR1927067     3  0.2345      0.723 0.000 0.100 0.900 0.000
#&gt; SRR1927064     1  0.0469      0.858 0.988 0.000 0.000 0.012
#&gt; SRR1927063     3  0.4790      0.343 0.000 0.380 0.620 0.000
#&gt; SRR1927062     4  0.0188      0.918 0.004 0.000 0.000 0.996
</code></pre>

<script>
$('#tab-CV-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-3-a').click(function(){
  $('#tab-CV-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-4'>
<p><a id='tab-CV-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1927048     1  0.2329     0.8458 0.876 0.124 0.000 0.000 0.000
#&gt; SRR1927061     3  0.0000     0.9967 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927060     1  0.2424     0.8437 0.868 0.132 0.000 0.000 0.000
#&gt; SRR1927059     5  0.0000     0.5359 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1927058     1  0.2230     0.8477 0.884 0.116 0.000 0.000 0.000
#&gt; SRR1927057     5  0.2773     0.4045 0.000 0.000 0.164 0.000 0.836
#&gt; SRR1927055     3  0.0000     0.9967 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927056     4  0.0000     0.8559 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927054     1  0.2424     0.8437 0.868 0.132 0.000 0.000 0.000
#&gt; SRR1927052     4  0.4302     0.1785 0.480 0.000 0.000 0.520 0.000
#&gt; SRR1927053     5  0.0000     0.5359 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1927051     2  0.4696     0.7915 0.000 0.556 0.016 0.000 0.428
#&gt; SRR1927050     4  0.0000     0.8559 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927049     2  0.5044     0.7908 0.000 0.556 0.036 0.000 0.408
#&gt; SRR1927047     5  0.3837    -0.1585 0.000 0.308 0.000 0.000 0.692
#&gt; SRR1927046     1  0.2377     0.7753 0.872 0.000 0.000 0.128 0.000
#&gt; SRR1927045     2  0.4268     0.1019 0.000 0.556 0.444 0.000 0.000
#&gt; SRR1927044     1  0.0880     0.8431 0.968 0.000 0.000 0.032 0.000
#&gt; SRR1927043     3  0.0000     0.9967 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927042     1  0.0000     0.8489 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.2424     0.8437 0.868 0.132 0.000 0.000 0.000
#&gt; SRR1927039     5  0.0000     0.5359 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1927038     1  0.2424     0.8437 0.868 0.132 0.000 0.000 0.000
#&gt; SRR1927037     5  0.1908     0.4177 0.000 0.092 0.000 0.000 0.908
#&gt; SRR1927036     1  0.3424     0.6378 0.760 0.000 0.000 0.240 0.000
#&gt; SRR1927035     5  0.4446    -0.6839 0.000 0.476 0.004 0.000 0.520
#&gt; SRR1927034     4  0.0000     0.8559 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927033     3  0.0290     0.9902 0.000 0.008 0.992 0.000 0.000
#&gt; SRR1927032     1  0.1845     0.8539 0.928 0.056 0.000 0.016 0.000
#&gt; SRR1927031     5  0.0000     0.5359 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1927030     1  0.1410     0.8299 0.940 0.000 0.000 0.060 0.000
#&gt; SRR1927028     4  0.3774     0.6412 0.296 0.000 0.000 0.704 0.000
#&gt; SRR1927029     3  0.0000     0.9967 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927027     5  0.8040     0.0732 0.000 0.312 0.288 0.084 0.316
#&gt; SRR1927026     4  0.0162     0.8555 0.004 0.000 0.000 0.996 0.000
#&gt; SRR1927024     4  0.3730     0.6531 0.288 0.000 0.000 0.712 0.000
#&gt; SRR1927025     5  0.6687     0.2351 0.000 0.332 0.248 0.000 0.420
#&gt; SRR1927023     5  0.6050     0.3797 0.000 0.312 0.144 0.000 0.544
#&gt; SRR1927022     1  0.3684     0.5599 0.720 0.000 0.000 0.280 0.000
#&gt; SRR1927021     2  0.4151     0.7031 0.000 0.652 0.004 0.000 0.344
#&gt; SRR1927020     4  0.0000     0.8559 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927019     2  0.4774     0.7945 0.000 0.556 0.020 0.000 0.424
#&gt; SRR1927071     4  0.0162     0.8555 0.004 0.000 0.000 0.996 0.000
#&gt; SRR1927069     2  0.4278     0.7610 0.000 0.548 0.000 0.000 0.452
#&gt; SRR1927070     1  0.3424     0.6378 0.760 0.000 0.000 0.240 0.000
#&gt; SRR1927068     4  0.0000     0.8559 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927066     4  0.3774     0.6412 0.296 0.000 0.000 0.704 0.000
#&gt; SRR1927065     3  0.0000     0.9967 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927067     3  0.0290     0.9892 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1927064     1  0.0404     0.8487 0.988 0.000 0.000 0.012 0.000
#&gt; SRR1927063     2  0.4924     0.7939 0.000 0.552 0.028 0.000 0.420
#&gt; SRR1927062     4  0.0162     0.8555 0.004 0.000 0.000 0.996 0.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-4-a').click(function(){
  $('#tab-CV-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-5'>
<p><a id='tab-CV-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1927048     1  0.4760     0.6664 0.668 0.212 0.000 0.000 0.120 0.000
#&gt; SRR1927061     3  0.0000     0.9917 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927060     1  0.5119     0.6089 0.584 0.308 0.000 0.000 0.108 0.000
#&gt; SRR1927059     6  0.0000     0.9234 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1927058     1  0.4946     0.6265 0.616 0.284 0.000 0.000 0.100 0.000
#&gt; SRR1927057     6  0.2048     0.7990 0.000 0.000 0.120 0.000 0.000 0.880
#&gt; SRR1927055     3  0.0000     0.9917 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927056     4  0.0000     0.8551 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927054     1  0.5119     0.6089 0.584 0.308 0.000 0.000 0.108 0.000
#&gt; SRR1927052     1  0.3601     0.3738 0.684 0.000 0.000 0.312 0.004 0.000
#&gt; SRR1927053     6  0.0000     0.9234 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1927051     2  0.3867     0.8435 0.000 0.660 0.012 0.000 0.000 0.328
#&gt; SRR1927050     4  0.0000     0.8551 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927049     2  0.4011     0.8394 0.000 0.672 0.024 0.000 0.000 0.304
#&gt; SRR1927047     6  0.2692     0.7280 0.000 0.148 0.000 0.000 0.012 0.840
#&gt; SRR1927046     1  0.3341     0.6928 0.836 0.020 0.000 0.048 0.096 0.000
#&gt; SRR1927045     2  0.3531     0.4168 0.000 0.672 0.328 0.000 0.000 0.000
#&gt; SRR1927044     1  0.0405     0.7453 0.988 0.000 0.000 0.008 0.004 0.000
#&gt; SRR1927043     3  0.0000     0.9917 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927042     1  0.0146     0.7447 0.996 0.004 0.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.5119     0.6089 0.584 0.308 0.000 0.000 0.108 0.000
#&gt; SRR1927039     6  0.0000     0.9234 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1927038     1  0.5119     0.6089 0.584 0.308 0.000 0.000 0.108 0.000
#&gt; SRR1927037     6  0.0713     0.9048 0.000 0.028 0.000 0.000 0.000 0.972
#&gt; SRR1927036     1  0.1644     0.7175 0.920 0.000 0.000 0.076 0.004 0.000
#&gt; SRR1927035     2  0.3847     0.6447 0.000 0.544 0.000 0.000 0.000 0.456
#&gt; SRR1927034     4  0.0000     0.8551 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927033     3  0.0790     0.9615 0.000 0.032 0.968 0.000 0.000 0.000
#&gt; SRR1927032     1  0.2673     0.7228 0.852 0.132 0.000 0.004 0.012 0.000
#&gt; SRR1927031     6  0.0000     0.9234 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1927030     1  0.0458     0.7448 0.984 0.000 0.000 0.016 0.000 0.000
#&gt; SRR1927028     4  0.3989     0.1349 0.468 0.000 0.000 0.528 0.004 0.000
#&gt; SRR1927029     3  0.0000     0.9917 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927027     5  0.3703     0.9195 0.000 0.000 0.064 0.008 0.796 0.132
#&gt; SRR1927026     4  0.0260     0.8530 0.008 0.000 0.000 0.992 0.000 0.000
#&gt; SRR1927024     1  0.5475     0.0727 0.500 0.016 0.000 0.404 0.080 0.000
#&gt; SRR1927025     5  0.3345     0.9461 0.000 0.000 0.028 0.000 0.788 0.184
#&gt; SRR1927023     5  0.3078     0.9346 0.000 0.012 0.000 0.000 0.796 0.192
#&gt; SRR1927022     1  0.3751     0.6691 0.808 0.020 0.000 0.080 0.092 0.000
#&gt; SRR1927021     2  0.4813     0.7655 0.000 0.648 0.000 0.000 0.104 0.248
#&gt; SRR1927020     4  0.0000     0.8551 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927019     2  0.3867     0.8435 0.000 0.660 0.012 0.000 0.000 0.328
#&gt; SRR1927071     4  0.0508     0.8495 0.012 0.000 0.000 0.984 0.004 0.000
#&gt; SRR1927069     2  0.3592     0.8305 0.000 0.656 0.000 0.000 0.000 0.344
#&gt; SRR1927070     1  0.1644     0.7175 0.920 0.000 0.000 0.076 0.004 0.000
#&gt; SRR1927068     4  0.0000     0.8551 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927066     4  0.3982     0.1495 0.460 0.000 0.000 0.536 0.004 0.000
#&gt; SRR1927065     3  0.0000     0.9917 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927067     3  0.0260     0.9841 0.000 0.000 0.992 0.000 0.000 0.008
#&gt; SRR1927064     1  0.0692     0.7439 0.976 0.000 0.000 0.004 0.020 0.000
#&gt; SRR1927063     2  0.3905     0.8437 0.000 0.668 0.016 0.000 0.000 0.316
#&gt; SRR1927062     4  0.0603     0.8475 0.016 0.000 0.000 0.980 0.004 0.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-5-a').click(function(){
  $('#tab-CV-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-pam-membership-heatmap'>
<ul>
<li><a href='#tab-CV-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-signatures'>
<ul>
<li><a href='#tab-CV-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-1-1.png" alt="plot of chunk tab-CV-pam-get-signatures-1"/></p>

</div>
<div id='tab-CV-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-2-1.png" alt="plot of chunk tab-CV-pam-get-signatures-2"/></p>

</div>
<div id='tab-CV-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-3-1.png" alt="plot of chunk tab-CV-pam-get-signatures-3"/></p>

</div>
<div id='tab-CV-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-4-1.png" alt="plot of chunk tab-CV-pam-get-signatures-4"/></p>

</div>
<div id='tab-CV-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-5-1.png" alt="plot of chunk tab-CV-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-pam-signature_compare](figure_cola/CV-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-pam-dimension-reduction'>
<ul>
<li><a href='#tab-CV-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-pam-collect-classes](figure_cola/CV-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:mclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "mclust"]
# you can also extract it by
# res = res_list["CV:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16868 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-mclust-collect-plots](figure_cola/CV-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-mclust-select-partition-number](figure_cola/CV-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5095 0.491   0.491
#> 3 3 0.734           0.860       0.848         0.2110 0.882   0.760
#> 4 4 0.631           0.418       0.714         0.0847 0.885   0.749
#> 5 5 0.833           0.886       0.929         0.1498 0.765   0.470
#> 6 6 0.854           0.779       0.886         0.0290 0.991   0.960
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-classes'>
<ul>
<li><a href='#tab-CV-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-mclust-get-classes-1'>
<p><a id='tab-CV-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1927048     1       0          1  1  0
#&gt; SRR1927061     2       0          1  0  1
#&gt; SRR1927060     1       0          1  1  0
#&gt; SRR1927059     2       0          1  0  1
#&gt; SRR1927058     1       0          1  1  0
#&gt; SRR1927057     2       0          1  0  1
#&gt; SRR1927055     2       0          1  0  1
#&gt; SRR1927056     1       0          1  1  0
#&gt; SRR1927054     1       0          1  1  0
#&gt; SRR1927052     1       0          1  1  0
#&gt; SRR1927053     2       0          1  0  1
#&gt; SRR1927051     2       0          1  0  1
#&gt; SRR1927050     1       0          1  1  0
#&gt; SRR1927049     2       0          1  0  1
#&gt; SRR1927047     2       0          1  0  1
#&gt; SRR1927046     1       0          1  1  0
#&gt; SRR1927045     2       0          1  0  1
#&gt; SRR1927044     1       0          1  1  0
#&gt; SRR1927043     2       0          1  0  1
#&gt; SRR1927042     1       0          1  1  0
#&gt; SRR1927040     1       0          1  1  0
#&gt; SRR1927039     2       0          1  0  1
#&gt; SRR1927038     1       0          1  1  0
#&gt; SRR1927037     2       0          1  0  1
#&gt; SRR1927036     1       0          1  1  0
#&gt; SRR1927035     2       0          1  0  1
#&gt; SRR1927034     1       0          1  1  0
#&gt; SRR1927033     2       0          1  0  1
#&gt; SRR1927032     1       0          1  1  0
#&gt; SRR1927031     2       0          1  0  1
#&gt; SRR1927030     1       0          1  1  0
#&gt; SRR1927028     1       0          1  1  0
#&gt; SRR1927029     2       0          1  0  1
#&gt; SRR1927027     2       0          1  0  1
#&gt; SRR1927026     1       0          1  1  0
#&gt; SRR1927024     1       0          1  1  0
#&gt; SRR1927025     2       0          1  0  1
#&gt; SRR1927023     2       0          1  0  1
#&gt; SRR1927022     1       0          1  1  0
#&gt; SRR1927021     2       0          1  0  1
#&gt; SRR1927020     1       0          1  1  0
#&gt; SRR1927019     2       0          1  0  1
#&gt; SRR1927071     1       0          1  1  0
#&gt; SRR1927069     2       0          1  0  1
#&gt; SRR1927070     1       0          1  1  0
#&gt; SRR1927068     1       0          1  1  0
#&gt; SRR1927066     1       0          1  1  0
#&gt; SRR1927065     2       0          1  0  1
#&gt; SRR1927067     2       0          1  0  1
#&gt; SRR1927064     1       0          1  1  0
#&gt; SRR1927063     2       0          1  0  1
#&gt; SRR1927062     1       0          1  1  0
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-1-a').click(function(){
  $('#tab-CV-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-2'>
<p><a id='tab-CV-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1927048     1  0.1163      0.945 0.972 0.000 0.028
#&gt; SRR1927061     2  0.1289      0.782 0.000 0.968 0.032
#&gt; SRR1927060     1  0.2711      0.934 0.912 0.000 0.088
#&gt; SRR1927059     3  0.5810      0.908 0.000 0.336 0.664
#&gt; SRR1927058     1  0.2537      0.936 0.920 0.000 0.080
#&gt; SRR1927057     3  0.6008      0.889 0.000 0.372 0.628
#&gt; SRR1927055     2  0.4887      0.727 0.000 0.772 0.228
#&gt; SRR1927056     1  0.2537      0.935 0.920 0.000 0.080
#&gt; SRR1927054     1  0.2796      0.933 0.908 0.000 0.092
#&gt; SRR1927052     1  0.1529      0.943 0.960 0.000 0.040
#&gt; SRR1927053     3  0.5810      0.908 0.000 0.336 0.664
#&gt; SRR1927051     2  0.5178      0.560 0.000 0.744 0.256
#&gt; SRR1927050     1  0.2537      0.935 0.920 0.000 0.080
#&gt; SRR1927049     2  0.3752      0.679 0.000 0.856 0.144
#&gt; SRR1927047     3  0.5760      0.905 0.000 0.328 0.672
#&gt; SRR1927046     1  0.0592      0.946 0.988 0.000 0.012
#&gt; SRR1927045     3  0.6204      0.746 0.000 0.424 0.576
#&gt; SRR1927044     1  0.2165      0.940 0.936 0.000 0.064
#&gt; SRR1927043     2  0.2625      0.767 0.000 0.916 0.084
#&gt; SRR1927042     1  0.2356      0.938 0.928 0.000 0.072
#&gt; SRR1927040     1  0.2711      0.934 0.912 0.000 0.088
#&gt; SRR1927039     3  0.5810      0.908 0.000 0.336 0.664
#&gt; SRR1927038     1  0.2711      0.934 0.912 0.000 0.088
#&gt; SRR1927037     3  0.5810      0.908 0.000 0.336 0.664
#&gt; SRR1927036     1  0.0592      0.947 0.988 0.000 0.012
#&gt; SRR1927035     3  0.5926      0.893 0.000 0.356 0.644
#&gt; SRR1927034     1  0.2448      0.936 0.924 0.000 0.076
#&gt; SRR1927033     3  0.6244      0.675 0.000 0.440 0.560
#&gt; SRR1927032     1  0.2448      0.938 0.924 0.000 0.076
#&gt; SRR1927031     3  0.5988      0.892 0.000 0.368 0.632
#&gt; SRR1927030     1  0.2165      0.940 0.936 0.000 0.064
#&gt; SRR1927028     1  0.2537      0.935 0.920 0.000 0.080
#&gt; SRR1927029     2  0.2537      0.769 0.000 0.920 0.080
#&gt; SRR1927027     2  0.4062      0.673 0.000 0.836 0.164
#&gt; SRR1927026     1  0.2537      0.935 0.920 0.000 0.080
#&gt; SRR1927024     1  0.1031      0.946 0.976 0.000 0.024
#&gt; SRR1927025     2  0.2356      0.745 0.000 0.928 0.072
#&gt; SRR1927023     2  0.4121      0.674 0.000 0.832 0.168
#&gt; SRR1927022     1  0.1031      0.946 0.976 0.000 0.024
#&gt; SRR1927021     3  0.6235      0.697 0.000 0.436 0.564
#&gt; SRR1927020     1  0.2537      0.935 0.920 0.000 0.080
#&gt; SRR1927019     2  0.5178      0.560 0.000 0.744 0.256
#&gt; SRR1927071     1  0.2448      0.936 0.924 0.000 0.076
#&gt; SRR1927069     3  0.5810      0.908 0.000 0.336 0.664
#&gt; SRR1927070     1  0.2066      0.941 0.940 0.000 0.060
#&gt; SRR1927068     1  0.2537      0.935 0.920 0.000 0.080
#&gt; SRR1927066     1  0.2537      0.935 0.920 0.000 0.080
#&gt; SRR1927065     2  0.3038      0.747 0.000 0.896 0.104
#&gt; SRR1927067     2  0.1411      0.782 0.000 0.964 0.036
#&gt; SRR1927064     1  0.2537      0.937 0.920 0.000 0.080
#&gt; SRR1927063     2  0.3752      0.679 0.000 0.856 0.144
#&gt; SRR1927062     1  0.2448      0.941 0.924 0.000 0.076
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-2-a').click(function(){
  $('#tab-CV-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-3'>
<p><a id='tab-CV-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1927048     1  0.6273     0.7379 0.636 0.000 0.100 0.264
#&gt; SRR1927061     2  0.1807     0.2522 0.000 0.940 0.052 0.008
#&gt; SRR1927060     1  0.6376     0.7150 0.536 0.000 0.068 0.396
#&gt; SRR1927059     2  0.4999    -0.1984 0.000 0.508 0.000 0.492
#&gt; SRR1927058     1  0.6367     0.7173 0.540 0.000 0.068 0.392
#&gt; SRR1927057     2  0.5376    -0.1172 0.000 0.588 0.016 0.396
#&gt; SRR1927055     2  0.3545     0.1793 0.000 0.828 0.164 0.008
#&gt; SRR1927056     1  0.0188     0.7818 0.996 0.000 0.000 0.004
#&gt; SRR1927054     1  0.6376     0.7150 0.536 0.000 0.068 0.396
#&gt; SRR1927052     1  0.0188     0.7839 0.996 0.000 0.000 0.004
#&gt; SRR1927053     2  0.5928    -0.2979 0.000 0.508 0.036 0.456
#&gt; SRR1927051     2  0.4981    -0.1563 0.000 0.536 0.000 0.464
#&gt; SRR1927050     1  0.0188     0.7818 0.996 0.000 0.000 0.004
#&gt; SRR1927049     2  0.5257    -0.1565 0.000 0.548 0.008 0.444
#&gt; SRR1927047     4  0.6120     0.2992 0.000 0.432 0.048 0.520
#&gt; SRR1927046     1  0.5280     0.7768 0.748 0.000 0.096 0.156
#&gt; SRR1927045     2  0.7490    -0.2448 0.000 0.496 0.220 0.284
#&gt; SRR1927044     1  0.5810     0.7695 0.660 0.000 0.064 0.276
#&gt; SRR1927043     2  0.0000     0.2716 0.000 1.000 0.000 0.000
#&gt; SRR1927042     1  0.6219     0.7432 0.588 0.000 0.068 0.344
#&gt; SRR1927040     1  0.6376     0.7150 0.536 0.000 0.068 0.396
#&gt; SRR1927039     2  0.6068    -0.3225 0.000 0.508 0.044 0.448
#&gt; SRR1927038     1  0.6376     0.7150 0.536 0.000 0.068 0.396
#&gt; SRR1927037     2  0.4999    -0.1984 0.000 0.508 0.000 0.492
#&gt; SRR1927036     1  0.3907     0.7928 0.768 0.000 0.000 0.232
#&gt; SRR1927035     2  0.5000    -0.2046 0.000 0.504 0.000 0.496
#&gt; SRR1927034     1  0.0657     0.7750 0.984 0.000 0.004 0.012
#&gt; SRR1927033     2  0.4501     0.0851 0.000 0.764 0.212 0.024
#&gt; SRR1927032     1  0.5189     0.7456 0.616 0.000 0.012 0.372
#&gt; SRR1927031     2  0.5376    -0.1172 0.000 0.588 0.016 0.396
#&gt; SRR1927030     1  0.5859     0.7673 0.652 0.000 0.064 0.284
#&gt; SRR1927028     1  0.0188     0.7818 0.996 0.000 0.000 0.004
#&gt; SRR1927029     2  0.0000     0.2716 0.000 1.000 0.000 0.000
#&gt; SRR1927027     3  0.5368     0.6988 0.000 0.340 0.636 0.024
#&gt; SRR1927026     1  0.0188     0.7818 0.996 0.000 0.000 0.004
#&gt; SRR1927024     1  0.3088     0.7400 0.864 0.000 0.128 0.008
#&gt; SRR1927025     2  0.6611    -0.0607 0.000 0.464 0.456 0.080
#&gt; SRR1927023     3  0.3970     0.6907 0.000 0.076 0.840 0.084
#&gt; SRR1927022     1  0.1635     0.7906 0.948 0.000 0.008 0.044
#&gt; SRR1927021     4  0.7558     0.4526 0.000 0.296 0.224 0.480
#&gt; SRR1927020     1  0.0188     0.7818 0.996 0.000 0.000 0.004
#&gt; SRR1927019     2  0.4977    -0.1535 0.000 0.540 0.000 0.460
#&gt; SRR1927071     1  0.0188     0.7839 0.996 0.000 0.000 0.004
#&gt; SRR1927069     2  0.5000    -0.2046 0.000 0.504 0.000 0.496
#&gt; SRR1927070     1  0.5759     0.7719 0.668 0.000 0.064 0.268
#&gt; SRR1927068     1  0.0188     0.7818 0.996 0.000 0.000 0.004
#&gt; SRR1927066     1  0.0336     0.7845 0.992 0.000 0.000 0.008
#&gt; SRR1927065     2  0.0000     0.2716 0.000 1.000 0.000 0.000
#&gt; SRR1927067     2  0.0921     0.2626 0.000 0.972 0.028 0.000
#&gt; SRR1927064     1  0.4936     0.7491 0.624 0.000 0.004 0.372
#&gt; SRR1927063     2  0.5257    -0.1565 0.000 0.548 0.008 0.444
#&gt; SRR1927062     1  0.4071     0.7894 0.832 0.000 0.064 0.104
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-3-a').click(function(){
  $('#tab-CV-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-4'>
<p><a id='tab-CV-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1927048     1  0.1281      0.835 0.956 0.000 0.000 0.032 0.012
#&gt; SRR1927061     3  0.3835      0.538 0.000 0.260 0.732 0.000 0.008
#&gt; SRR1927060     1  0.1270      0.901 0.948 0.000 0.000 0.052 0.000
#&gt; SRR1927059     2  0.0000      0.928 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927058     1  0.1908      0.902 0.908 0.000 0.000 0.092 0.000
#&gt; SRR1927057     2  0.2891      0.794 0.000 0.824 0.176 0.000 0.000
#&gt; SRR1927055     3  0.0290      0.871 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1927056     4  0.0000      0.970 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927054     1  0.1270      0.901 0.948 0.000 0.000 0.052 0.000
#&gt; SRR1927052     4  0.0963      0.945 0.036 0.000 0.000 0.964 0.000
#&gt; SRR1927053     2  0.0162      0.928 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1927051     2  0.1270      0.920 0.000 0.948 0.052 0.000 0.000
#&gt; SRR1927050     4  0.0000      0.970 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927049     2  0.3180      0.872 0.000 0.856 0.068 0.000 0.076
#&gt; SRR1927047     2  0.0162      0.928 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1927046     1  0.3690      0.720 0.764 0.000 0.000 0.224 0.012
#&gt; SRR1927045     2  0.2331      0.891 0.000 0.900 0.020 0.000 0.080
#&gt; SRR1927044     1  0.3039      0.867 0.808 0.000 0.000 0.192 0.000
#&gt; SRR1927043     3  0.0693      0.870 0.000 0.012 0.980 0.000 0.008
#&gt; SRR1927042     1  0.2424      0.895 0.868 0.000 0.000 0.132 0.000
#&gt; SRR1927040     1  0.1270      0.901 0.948 0.000 0.000 0.052 0.000
#&gt; SRR1927039     2  0.0162      0.928 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1927038     1  0.1270      0.901 0.948 0.000 0.000 0.052 0.000
#&gt; SRR1927037     2  0.0880      0.925 0.000 0.968 0.032 0.000 0.000
#&gt; SRR1927036     1  0.3003      0.871 0.812 0.000 0.000 0.188 0.000
#&gt; SRR1927035     2  0.0609      0.927 0.000 0.980 0.020 0.000 0.000
#&gt; SRR1927034     4  0.0000      0.970 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927033     3  0.0162      0.872 0.000 0.004 0.996 0.000 0.000
#&gt; SRR1927032     1  0.1544      0.900 0.932 0.000 0.000 0.068 0.000
#&gt; SRR1927031     2  0.0162      0.929 0.000 0.996 0.004 0.000 0.000
#&gt; SRR1927030     1  0.3003      0.871 0.812 0.000 0.000 0.188 0.000
#&gt; SRR1927028     4  0.0290      0.968 0.008 0.000 0.000 0.992 0.000
#&gt; SRR1927029     3  0.0693      0.870 0.000 0.012 0.980 0.000 0.008
#&gt; SRR1927027     5  0.1197      0.941 0.000 0.000 0.048 0.000 0.952
#&gt; SRR1927026     4  0.0000      0.970 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927024     4  0.2390      0.879 0.084 0.000 0.000 0.896 0.020
#&gt; SRR1927025     3  0.5180      0.408 0.000 0.064 0.624 0.000 0.312
#&gt; SRR1927023     5  0.0162      0.943 0.004 0.000 0.000 0.000 0.996
#&gt; SRR1927022     4  0.1942      0.919 0.068 0.000 0.000 0.920 0.012
#&gt; SRR1927021     2  0.3452      0.710 0.000 0.756 0.000 0.000 0.244
#&gt; SRR1927020     4  0.0162      0.970 0.004 0.000 0.000 0.996 0.000
#&gt; SRR1927019     2  0.1410      0.916 0.000 0.940 0.060 0.000 0.000
#&gt; SRR1927071     4  0.0000      0.970 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927069     2  0.0000      0.928 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927070     1  0.2966      0.873 0.816 0.000 0.000 0.184 0.000
#&gt; SRR1927068     4  0.0162      0.970 0.004 0.000 0.000 0.996 0.000
#&gt; SRR1927066     4  0.0162      0.970 0.004 0.000 0.000 0.996 0.000
#&gt; SRR1927065     3  0.0162      0.872 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1927067     3  0.0000      0.872 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927064     1  0.1478      0.900 0.936 0.000 0.000 0.064 0.000
#&gt; SRR1927063     2  0.3535      0.852 0.000 0.832 0.088 0.000 0.080
#&gt; SRR1927062     4  0.1732      0.904 0.080 0.000 0.000 0.920 0.000
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-4-a').click(function(){
  $('#tab-CV-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-5'>
<p><a id='tab-CV-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1927048     1  0.4615      0.253 0.536 0.000 0.000 0.040 0.000 0.424
#&gt; SRR1927061     3  0.4881      0.301 0.000 0.356 0.580 0.000 0.004 0.060
#&gt; SRR1927060     1  0.0603      0.886 0.980 0.000 0.000 0.016 0.000 0.004
#&gt; SRR1927059     2  0.1950      0.880 0.000 0.912 0.024 0.000 0.000 0.064
#&gt; SRR1927058     1  0.1152      0.885 0.952 0.000 0.000 0.044 0.000 0.004
#&gt; SRR1927057     2  0.3979      0.624 0.000 0.708 0.256 0.000 0.000 0.036
#&gt; SRR1927055     3  0.0603      0.817 0.000 0.004 0.980 0.000 0.016 0.000
#&gt; SRR1927056     4  0.1007      0.864 0.044 0.000 0.000 0.956 0.000 0.000
#&gt; SRR1927054     1  0.0405      0.882 0.988 0.000 0.000 0.004 0.000 0.008
#&gt; SRR1927052     4  0.1285      0.856 0.052 0.000 0.000 0.944 0.000 0.004
#&gt; SRR1927053     2  0.2066      0.878 0.000 0.904 0.024 0.000 0.000 0.072
#&gt; SRR1927051     2  0.2118      0.868 0.000 0.888 0.008 0.000 0.000 0.104
#&gt; SRR1927050     4  0.0260      0.893 0.008 0.000 0.000 0.992 0.000 0.000
#&gt; SRR1927049     2  0.2512      0.862 0.000 0.868 0.008 0.000 0.008 0.116
#&gt; SRR1927047     2  0.1588      0.878 0.000 0.924 0.000 0.004 0.000 0.072
#&gt; SRR1927046     1  0.4939      0.192 0.496 0.000 0.000 0.064 0.000 0.440
#&gt; SRR1927045     2  0.2393      0.854 0.000 0.884 0.004 0.000 0.092 0.020
#&gt; SRR1927044     1  0.1728      0.878 0.924 0.000 0.000 0.064 0.004 0.008
#&gt; SRR1927043     3  0.1464      0.813 0.000 0.016 0.944 0.000 0.004 0.036
#&gt; SRR1927042     1  0.1267      0.882 0.940 0.000 0.000 0.060 0.000 0.000
#&gt; SRR1927040     1  0.0405      0.885 0.988 0.000 0.000 0.008 0.000 0.004
#&gt; SRR1927039     2  0.2066      0.878 0.000 0.904 0.024 0.000 0.000 0.072
#&gt; SRR1927038     1  0.0405      0.885 0.988 0.000 0.000 0.008 0.000 0.004
#&gt; SRR1927037     2  0.2019      0.874 0.000 0.900 0.012 0.000 0.000 0.088
#&gt; SRR1927036     1  0.1643      0.876 0.924 0.000 0.000 0.068 0.000 0.008
#&gt; SRR1927035     2  0.1075      0.881 0.000 0.952 0.000 0.000 0.000 0.048
#&gt; SRR1927034     4  0.0405      0.889 0.008 0.000 0.000 0.988 0.000 0.004
#&gt; SRR1927033     3  0.2685      0.769 0.000 0.044 0.872 0.004 0.080 0.000
#&gt; SRR1927032     1  0.0260      0.883 0.992 0.000 0.000 0.008 0.000 0.000
#&gt; SRR1927031     2  0.2912      0.857 0.000 0.852 0.072 0.000 0.000 0.076
#&gt; SRR1927030     1  0.1584      0.879 0.928 0.000 0.000 0.064 0.000 0.008
#&gt; SRR1927028     4  0.0260      0.893 0.008 0.000 0.000 0.992 0.000 0.000
#&gt; SRR1927029     3  0.1464      0.813 0.000 0.016 0.944 0.000 0.004 0.036
#&gt; SRR1927027     5  0.1082      0.803 0.000 0.000 0.040 0.004 0.956 0.000
#&gt; SRR1927026     4  0.0260      0.893 0.008 0.000 0.000 0.992 0.000 0.000
#&gt; SRR1927024     6  0.4382      0.000 0.020 0.000 0.000 0.360 0.008 0.612
#&gt; SRR1927025     3  0.5115      0.594 0.000 0.076 0.696 0.000 0.168 0.060
#&gt; SRR1927023     5  0.3023      0.798 0.000 0.000 0.000 0.004 0.784 0.212
#&gt; SRR1927022     4  0.5065     -0.137 0.124 0.000 0.000 0.616 0.000 0.260
#&gt; SRR1927021     2  0.3047      0.852 0.000 0.848 0.000 0.004 0.064 0.084
#&gt; SRR1927020     4  0.0260      0.893 0.008 0.000 0.000 0.992 0.000 0.000
#&gt; SRR1927019     2  0.2165      0.867 0.000 0.884 0.008 0.000 0.000 0.108
#&gt; SRR1927071     4  0.0405      0.889 0.008 0.000 0.000 0.988 0.000 0.004
#&gt; SRR1927069     2  0.1387      0.879 0.000 0.932 0.000 0.000 0.000 0.068
#&gt; SRR1927070     1  0.1584      0.879 0.928 0.000 0.000 0.064 0.000 0.008
#&gt; SRR1927068     4  0.0260      0.893 0.008 0.000 0.000 0.992 0.000 0.000
#&gt; SRR1927066     4  0.0790      0.877 0.032 0.000 0.000 0.968 0.000 0.000
#&gt; SRR1927065     3  0.0000      0.817 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927067     3  0.0146      0.819 0.000 0.004 0.996 0.000 0.000 0.000
#&gt; SRR1927064     1  0.0622      0.882 0.980 0.000 0.000 0.012 0.000 0.008
#&gt; SRR1927063     2  0.2566      0.862 0.000 0.868 0.012 0.000 0.008 0.112
#&gt; SRR1927062     4  0.2595      0.655 0.160 0.000 0.000 0.836 0.000 0.004
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-5-a').click(function(){
  $('#tab-CV-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-CV-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-signatures'>
<ul>
<li><a href='#tab-CV-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-1-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-1"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-2-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-2"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-3-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-3"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-4-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-4"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-5-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-mclust-signature_compare](figure_cola/CV-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-CV-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-mclust-collect-classes](figure_cola/CV-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:NMF**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "NMF"]
# you can also extract it by
# res = res_list["CV:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16868 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-NMF-collect-plots](figure_cola/CV-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-NMF-select-partition-number](figure_cola/CV-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5095 0.491   0.491
#> 3 3 0.752           0.827       0.905         0.1335 0.965   0.929
#> 4 4 0.707           0.553       0.815         0.1394 0.913   0.810
#> 5 5 0.759           0.838       0.883         0.1429 0.778   0.454
#> 6 6 0.820           0.806       0.889         0.0442 0.954   0.802
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-classes'>
<ul>
<li><a href='#tab-CV-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-NMF-get-classes-1'>
<p><a id='tab-CV-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1927048     1       0          1  1  0
#&gt; SRR1927061     2       0          1  0  1
#&gt; SRR1927060     1       0          1  1  0
#&gt; SRR1927059     2       0          1  0  1
#&gt; SRR1927058     1       0          1  1  0
#&gt; SRR1927057     2       0          1  0  1
#&gt; SRR1927055     2       0          1  0  1
#&gt; SRR1927056     1       0          1  1  0
#&gt; SRR1927054     1       0          1  1  0
#&gt; SRR1927052     1       0          1  1  0
#&gt; SRR1927053     2       0          1  0  1
#&gt; SRR1927051     2       0          1  0  1
#&gt; SRR1927050     1       0          1  1  0
#&gt; SRR1927049     2       0          1  0  1
#&gt; SRR1927047     2       0          1  0  1
#&gt; SRR1927046     1       0          1  1  0
#&gt; SRR1927045     2       0          1  0  1
#&gt; SRR1927044     1       0          1  1  0
#&gt; SRR1927043     2       0          1  0  1
#&gt; SRR1927042     1       0          1  1  0
#&gt; SRR1927040     1       0          1  1  0
#&gt; SRR1927039     2       0          1  0  1
#&gt; SRR1927038     1       0          1  1  0
#&gt; SRR1927037     2       0          1  0  1
#&gt; SRR1927036     1       0          1  1  0
#&gt; SRR1927035     2       0          1  0  1
#&gt; SRR1927034     1       0          1  1  0
#&gt; SRR1927033     2       0          1  0  1
#&gt; SRR1927032     1       0          1  1  0
#&gt; SRR1927031     2       0          1  0  1
#&gt; SRR1927030     1       0          1  1  0
#&gt; SRR1927028     1       0          1  1  0
#&gt; SRR1927029     2       0          1  0  1
#&gt; SRR1927027     2       0          1  0  1
#&gt; SRR1927026     1       0          1  1  0
#&gt; SRR1927024     1       0          1  1  0
#&gt; SRR1927025     2       0          1  0  1
#&gt; SRR1927023     2       0          1  0  1
#&gt; SRR1927022     1       0          1  1  0
#&gt; SRR1927021     2       0          1  0  1
#&gt; SRR1927020     1       0          1  1  0
#&gt; SRR1927019     2       0          1  0  1
#&gt; SRR1927071     1       0          1  1  0
#&gt; SRR1927069     2       0          1  0  1
#&gt; SRR1927070     1       0          1  1  0
#&gt; SRR1927068     1       0          1  1  0
#&gt; SRR1927066     1       0          1  1  0
#&gt; SRR1927065     2       0          1  0  1
#&gt; SRR1927067     2       0          1  0  1
#&gt; SRR1927064     1       0          1  1  0
#&gt; SRR1927063     2       0          1  0  1
#&gt; SRR1927062     1       0          1  1  0
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-1-a').click(function(){
  $('#tab-CV-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-2'>
<p><a id='tab-CV-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1927048     1  0.0424      0.925 0.992 0.000 0.008
#&gt; SRR1927061     2  0.0424      0.849 0.000 0.992 0.008
#&gt; SRR1927060     1  0.0000      0.925 1.000 0.000 0.000
#&gt; SRR1927059     2  0.4399      0.662 0.000 0.812 0.188
#&gt; SRR1927058     1  0.0000      0.925 1.000 0.000 0.000
#&gt; SRR1927057     2  0.0000      0.850 0.000 1.000 0.000
#&gt; SRR1927055     2  0.0424      0.849 0.000 0.992 0.008
#&gt; SRR1927056     1  0.3619      0.913 0.864 0.000 0.136
#&gt; SRR1927054     1  0.0000      0.925 1.000 0.000 0.000
#&gt; SRR1927052     1  0.3619      0.913 0.864 0.000 0.136
#&gt; SRR1927053     2  0.6280     -0.601 0.000 0.540 0.460
#&gt; SRR1927051     2  0.0000      0.850 0.000 1.000 0.000
#&gt; SRR1927050     1  0.4702      0.874 0.788 0.000 0.212
#&gt; SRR1927049     2  0.0237      0.850 0.000 0.996 0.004
#&gt; SRR1927047     2  0.3941      0.725 0.000 0.844 0.156
#&gt; SRR1927046     1  0.1860      0.923 0.948 0.000 0.052
#&gt; SRR1927045     2  0.0000      0.850 0.000 1.000 0.000
#&gt; SRR1927044     1  0.0000      0.925 1.000 0.000 0.000
#&gt; SRR1927043     2  0.0424      0.849 0.000 0.992 0.008
#&gt; SRR1927042     1  0.0000      0.925 1.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      0.925 1.000 0.000 0.000
#&gt; SRR1927039     3  0.6252      0.739 0.000 0.444 0.556
#&gt; SRR1927038     1  0.0000      0.925 1.000 0.000 0.000
#&gt; SRR1927037     2  0.2356      0.812 0.000 0.928 0.072
#&gt; SRR1927036     1  0.0000      0.925 1.000 0.000 0.000
#&gt; SRR1927035     2  0.2356      0.812 0.000 0.928 0.072
#&gt; SRR1927034     1  0.5431      0.816 0.716 0.000 0.284
#&gt; SRR1927033     2  0.0424      0.849 0.000 0.992 0.008
#&gt; SRR1927032     1  0.0000      0.925 1.000 0.000 0.000
#&gt; SRR1927031     2  0.3879      0.731 0.000 0.848 0.152
#&gt; SRR1927030     1  0.0000      0.925 1.000 0.000 0.000
#&gt; SRR1927028     1  0.3619      0.913 0.864 0.000 0.136
#&gt; SRR1927029     2  0.0424      0.849 0.000 0.992 0.008
#&gt; SRR1927027     2  0.4842      0.589 0.000 0.776 0.224
#&gt; SRR1927026     1  0.4702      0.874 0.788 0.000 0.212
#&gt; SRR1927024     1  0.5835      0.759 0.660 0.000 0.340
#&gt; SRR1927025     2  0.3752      0.742 0.000 0.856 0.144
#&gt; SRR1927023     3  0.5988      0.773 0.000 0.368 0.632
#&gt; SRR1927022     1  0.3619      0.913 0.864 0.000 0.136
#&gt; SRR1927021     2  0.3816      0.737 0.000 0.852 0.148
#&gt; SRR1927020     1  0.4346      0.891 0.816 0.000 0.184
#&gt; SRR1927019     2  0.0000      0.850 0.000 1.000 0.000
#&gt; SRR1927071     1  0.3619      0.913 0.864 0.000 0.136
#&gt; SRR1927069     2  0.3686      0.747 0.000 0.860 0.140
#&gt; SRR1927070     1  0.0000      0.925 1.000 0.000 0.000
#&gt; SRR1927068     1  0.3619      0.913 0.864 0.000 0.136
#&gt; SRR1927066     1  0.3619      0.913 0.864 0.000 0.136
#&gt; SRR1927065     2  0.0424      0.849 0.000 0.992 0.008
#&gt; SRR1927067     2  0.0424      0.849 0.000 0.992 0.008
#&gt; SRR1927064     1  0.0000      0.925 1.000 0.000 0.000
#&gt; SRR1927063     2  0.0424      0.849 0.000 0.992 0.008
#&gt; SRR1927062     1  0.2796      0.919 0.908 0.000 0.092
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-2-a').click(function(){
  $('#tab-CV-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-3'>
<p><a id='tab-CV-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1927048     1  0.0188     0.6882 0.996 0.000 0.000 0.004
#&gt; SRR1927061     2  0.0469     0.7990 0.000 0.988 0.012 0.000
#&gt; SRR1927060     1  0.0000     0.6898 1.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.4925     0.1068 0.000 0.572 0.428 0.000
#&gt; SRR1927058     1  0.0000     0.6898 1.000 0.000 0.000 0.000
#&gt; SRR1927057     2  0.1118     0.7948 0.000 0.964 0.036 0.000
#&gt; SRR1927055     2  0.0779     0.7943 0.000 0.980 0.016 0.004
#&gt; SRR1927056     1  0.4843     0.3889 0.604 0.000 0.000 0.396
#&gt; SRR1927054     1  0.0000     0.6898 1.000 0.000 0.000 0.000
#&gt; SRR1927052     1  0.4804     0.4019 0.616 0.000 0.000 0.384
#&gt; SRR1927053     3  0.4164     0.5595 0.000 0.264 0.736 0.000
#&gt; SRR1927051     2  0.0817     0.8005 0.000 0.976 0.024 0.000
#&gt; SRR1927050     1  0.4843     0.3889 0.604 0.000 0.000 0.396
#&gt; SRR1927049     2  0.0469     0.8034 0.000 0.988 0.012 0.000
#&gt; SRR1927047     3  0.5000    -0.0446 0.000 0.496 0.504 0.000
#&gt; SRR1927046     1  0.3726     0.5636 0.788 0.000 0.000 0.212
#&gt; SRR1927045     2  0.0469     0.8034 0.000 0.988 0.012 0.000
#&gt; SRR1927044     1  0.0000     0.6898 1.000 0.000 0.000 0.000
#&gt; SRR1927043     2  0.0469     0.7990 0.000 0.988 0.012 0.000
#&gt; SRR1927042     1  0.0000     0.6898 1.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0000     0.6898 1.000 0.000 0.000 0.000
#&gt; SRR1927039     3  0.2760     0.6347 0.000 0.128 0.872 0.000
#&gt; SRR1927038     1  0.0000     0.6898 1.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.2921     0.7057 0.000 0.860 0.140 0.000
#&gt; SRR1927036     1  0.0000     0.6898 1.000 0.000 0.000 0.000
#&gt; SRR1927035     2  0.2530     0.7361 0.000 0.888 0.112 0.000
#&gt; SRR1927034     4  0.4907    -0.0476 0.420 0.000 0.000 0.580
#&gt; SRR1927033     2  0.0927     0.7911 0.000 0.976 0.016 0.008
#&gt; SRR1927032     1  0.0000     0.6898 1.000 0.000 0.000 0.000
#&gt; SRR1927031     2  0.4817     0.2294 0.000 0.612 0.388 0.000
#&gt; SRR1927030     1  0.0000     0.6898 1.000 0.000 0.000 0.000
#&gt; SRR1927028     1  0.4843     0.3889 0.604 0.000 0.000 0.396
#&gt; SRR1927029     2  0.0779     0.7943 0.000 0.980 0.016 0.004
#&gt; SRR1927027     3  0.7448     0.6180 0.000 0.172 0.428 0.400
#&gt; SRR1927026     1  0.4855     0.3768 0.600 0.000 0.000 0.400
#&gt; SRR1927024     4  0.1940     0.3698 0.076 0.000 0.000 0.924
#&gt; SRR1927025     2  0.5285    -0.0848 0.000 0.524 0.468 0.008
#&gt; SRR1927023     3  0.5279     0.5047 0.000 0.012 0.588 0.400
#&gt; SRR1927022     1  0.4843     0.3889 0.604 0.000 0.000 0.396
#&gt; SRR1927021     2  0.5288    -0.1002 0.000 0.520 0.472 0.008
#&gt; SRR1927020     1  0.4843     0.3889 0.604 0.000 0.000 0.396
#&gt; SRR1927019     2  0.0707     0.8019 0.000 0.980 0.020 0.000
#&gt; SRR1927071     1  0.4843     0.3889 0.604 0.000 0.000 0.396
#&gt; SRR1927069     2  0.4790     0.2528 0.000 0.620 0.380 0.000
#&gt; SRR1927070     1  0.0000     0.6898 1.000 0.000 0.000 0.000
#&gt; SRR1927068     1  0.4843     0.3889 0.604 0.000 0.000 0.396
#&gt; SRR1927066     1  0.4843     0.3889 0.604 0.000 0.000 0.396
#&gt; SRR1927065     2  0.0336     0.8006 0.000 0.992 0.008 0.000
#&gt; SRR1927067     2  0.0188     0.8033 0.000 0.996 0.004 0.000
#&gt; SRR1927064     1  0.0000     0.6898 1.000 0.000 0.000 0.000
#&gt; SRR1927063     2  0.0000     0.8028 0.000 1.000 0.000 0.000
#&gt; SRR1927062     1  0.4134     0.5214 0.740 0.000 0.000 0.260
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-3-a').click(function(){
  $('#tab-CV-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-4'>
<p><a id='tab-CV-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1927048     1  0.0955      0.910 0.968 0.000 0.000 0.028 0.004
#&gt; SRR1927061     3  0.0451      0.901 0.000 0.008 0.988 0.004 0.000
#&gt; SRR1927060     1  0.0000      0.940 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.1991      0.848 0.000 0.916 0.076 0.004 0.004
#&gt; SRR1927058     1  0.0880      0.944 0.968 0.000 0.000 0.032 0.000
#&gt; SRR1927057     2  0.3160      0.783 0.000 0.808 0.188 0.004 0.000
#&gt; SRR1927055     3  0.0000      0.897 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927056     4  0.3109      0.967 0.200 0.000 0.000 0.800 0.000
#&gt; SRR1927054     1  0.0290      0.940 0.992 0.000 0.000 0.008 0.000
#&gt; SRR1927052     4  0.3143      0.965 0.204 0.000 0.000 0.796 0.000
#&gt; SRR1927053     2  0.0960      0.809 0.000 0.972 0.016 0.004 0.008
#&gt; SRR1927051     2  0.4403      0.312 0.000 0.560 0.436 0.000 0.004
#&gt; SRR1927050     4  0.2516      0.927 0.140 0.000 0.000 0.860 0.000
#&gt; SRR1927049     3  0.2179      0.856 0.000 0.112 0.888 0.000 0.000
#&gt; SRR1927047     2  0.2054      0.836 0.000 0.920 0.052 0.000 0.028
#&gt; SRR1927046     1  0.0880      0.943 0.968 0.000 0.000 0.032 0.000
#&gt; SRR1927045     3  0.1704      0.892 0.000 0.068 0.928 0.000 0.004
#&gt; SRR1927044     1  0.0963      0.942 0.964 0.000 0.000 0.036 0.000
#&gt; SRR1927043     3  0.0451      0.901 0.000 0.008 0.988 0.004 0.000
#&gt; SRR1927042     1  0.0794      0.945 0.972 0.000 0.000 0.028 0.000
#&gt; SRR1927040     1  0.0290      0.934 0.992 0.000 0.000 0.008 0.000
#&gt; SRR1927039     2  0.0290      0.800 0.000 0.992 0.008 0.000 0.000
#&gt; SRR1927038     1  0.0000      0.940 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.2233      0.842 0.000 0.892 0.104 0.004 0.000
#&gt; SRR1927036     1  0.0880      0.944 0.968 0.000 0.000 0.032 0.000
#&gt; SRR1927035     2  0.3707      0.676 0.000 0.716 0.284 0.000 0.000
#&gt; SRR1927034     4  0.2280      0.901 0.120 0.000 0.000 0.880 0.000
#&gt; SRR1927033     3  0.0290      0.895 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1927032     1  0.0703      0.945 0.976 0.000 0.000 0.024 0.000
#&gt; SRR1927031     2  0.1608      0.846 0.000 0.928 0.072 0.000 0.000
#&gt; SRR1927030     1  0.0963      0.942 0.964 0.000 0.000 0.036 0.000
#&gt; SRR1927028     4  0.2852      0.956 0.172 0.000 0.000 0.828 0.000
#&gt; SRR1927029     3  0.0162      0.897 0.000 0.000 0.996 0.004 0.000
#&gt; SRR1927027     5  0.4562      0.366 0.000 0.444 0.004 0.004 0.548
#&gt; SRR1927026     4  0.2813      0.953 0.168 0.000 0.000 0.832 0.000
#&gt; SRR1927024     5  0.3727      0.536 0.016 0.000 0.000 0.216 0.768
#&gt; SRR1927025     2  0.2144      0.795 0.000 0.912 0.020 0.000 0.068
#&gt; SRR1927023     5  0.3074      0.659 0.000 0.196 0.000 0.000 0.804
#&gt; SRR1927022     1  0.4138      0.156 0.616 0.000 0.000 0.384 0.000
#&gt; SRR1927021     2  0.3670      0.798 0.000 0.820 0.112 0.000 0.068
#&gt; SRR1927020     4  0.3003      0.965 0.188 0.000 0.000 0.812 0.000
#&gt; SRR1927019     3  0.4235      0.115 0.000 0.424 0.576 0.000 0.000
#&gt; SRR1927071     4  0.3109      0.967 0.200 0.000 0.000 0.800 0.000
#&gt; SRR1927069     2  0.1792      0.847 0.000 0.916 0.084 0.000 0.000
#&gt; SRR1927070     1  0.1043      0.939 0.960 0.000 0.000 0.040 0.000
#&gt; SRR1927068     4  0.3109      0.967 0.200 0.000 0.000 0.800 0.000
#&gt; SRR1927066     4  0.3143      0.965 0.204 0.000 0.000 0.796 0.000
#&gt; SRR1927065     3  0.1608      0.892 0.000 0.072 0.928 0.000 0.000
#&gt; SRR1927067     3  0.1768      0.892 0.000 0.072 0.924 0.004 0.000
#&gt; SRR1927064     1  0.0162      0.941 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1927063     3  0.0794      0.902 0.000 0.028 0.972 0.000 0.000
#&gt; SRR1927062     4  0.3274      0.949 0.220 0.000 0.000 0.780 0.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-4-a').click(function(){
  $('#tab-CV-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-5'>
<p><a id='tab-CV-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1927048     1  0.1501      0.910 0.924 0.000 0.000 0.000 0.000 0.076
#&gt; SRR1927061     3  0.0653      0.962 0.000 0.004 0.980 0.000 0.004 0.012
#&gt; SRR1927060     1  0.0000      0.964 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.0622      0.714 0.000 0.980 0.012 0.000 0.008 0.000
#&gt; SRR1927058     1  0.0520      0.964 0.984 0.000 0.000 0.008 0.000 0.008
#&gt; SRR1927057     2  0.4012      0.639 0.000 0.716 0.252 0.000 0.016 0.016
#&gt; SRR1927055     3  0.0551      0.961 0.000 0.000 0.984 0.004 0.008 0.004
#&gt; SRR1927056     4  0.2163      0.875 0.092 0.000 0.000 0.892 0.000 0.016
#&gt; SRR1927054     1  0.0405      0.964 0.988 0.000 0.000 0.008 0.000 0.004
#&gt; SRR1927052     4  0.1958      0.873 0.100 0.000 0.000 0.896 0.000 0.004
#&gt; SRR1927053     2  0.0870      0.704 0.000 0.972 0.004 0.000 0.012 0.012
#&gt; SRR1927051     2  0.4181      0.515 0.000 0.600 0.384 0.000 0.012 0.004
#&gt; SRR1927050     4  0.1268      0.834 0.036 0.000 0.000 0.952 0.004 0.008
#&gt; SRR1927049     3  0.2561      0.869 0.000 0.092 0.880 0.004 0.008 0.016
#&gt; SRR1927047     2  0.1820      0.734 0.000 0.924 0.056 0.000 0.012 0.008
#&gt; SRR1927046     1  0.2632      0.820 0.832 0.000 0.000 0.004 0.000 0.164
#&gt; SRR1927045     3  0.1148      0.958 0.000 0.000 0.960 0.004 0.020 0.016
#&gt; SRR1927044     1  0.1245      0.950 0.952 0.000 0.000 0.016 0.000 0.032
#&gt; SRR1927043     3  0.0653      0.962 0.000 0.004 0.980 0.000 0.004 0.012
#&gt; SRR1927042     1  0.0291      0.965 0.992 0.000 0.000 0.004 0.000 0.004
#&gt; SRR1927040     1  0.0000      0.964 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927039     2  0.1152      0.698 0.000 0.952 0.000 0.000 0.044 0.004
#&gt; SRR1927038     1  0.0000      0.964 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.1858      0.734 0.000 0.904 0.092 0.000 0.000 0.004
#&gt; SRR1927036     1  0.1010      0.947 0.960 0.000 0.000 0.036 0.000 0.004
#&gt; SRR1927035     2  0.3240      0.664 0.000 0.752 0.244 0.000 0.004 0.000
#&gt; SRR1927034     4  0.0881      0.788 0.012 0.000 0.000 0.972 0.008 0.008
#&gt; SRR1927033     3  0.1511      0.942 0.000 0.000 0.940 0.004 0.044 0.012
#&gt; SRR1927032     1  0.0291      0.965 0.992 0.000 0.000 0.004 0.000 0.004
#&gt; SRR1927031     2  0.2121      0.682 0.000 0.892 0.012 0.000 0.096 0.000
#&gt; SRR1927030     1  0.1564      0.937 0.936 0.000 0.000 0.024 0.000 0.040
#&gt; SRR1927028     4  0.1297      0.843 0.040 0.000 0.000 0.948 0.000 0.012
#&gt; SRR1927029     3  0.0363      0.962 0.000 0.000 0.988 0.000 0.000 0.012
#&gt; SRR1927027     5  0.2278      0.657 0.000 0.128 0.000 0.004 0.868 0.000
#&gt; SRR1927026     4  0.2164      0.861 0.068 0.000 0.000 0.900 0.000 0.032
#&gt; SRR1927024     6  0.5615      0.000 0.008 0.000 0.000 0.296 0.144 0.552
#&gt; SRR1927025     5  0.3756      0.568 0.000 0.400 0.000 0.000 0.600 0.000
#&gt; SRR1927023     5  0.4319      0.664 0.000 0.168 0.000 0.000 0.724 0.108
#&gt; SRR1927022     4  0.4493      0.308 0.364 0.000 0.000 0.596 0.000 0.040
#&gt; SRR1927021     2  0.5820      0.462 0.000 0.612 0.116 0.000 0.056 0.216
#&gt; SRR1927020     4  0.1349      0.859 0.056 0.000 0.000 0.940 0.000 0.004
#&gt; SRR1927019     2  0.3982      0.357 0.000 0.536 0.460 0.000 0.000 0.004
#&gt; SRR1927071     4  0.1967      0.876 0.084 0.000 0.000 0.904 0.000 0.012
#&gt; SRR1927069     2  0.1807      0.711 0.000 0.920 0.020 0.000 0.060 0.000
#&gt; SRR1927070     1  0.0914      0.960 0.968 0.000 0.000 0.016 0.000 0.016
#&gt; SRR1927068     4  0.2121      0.874 0.096 0.000 0.000 0.892 0.000 0.012
#&gt; SRR1927066     4  0.2510      0.865 0.100 0.000 0.000 0.872 0.000 0.028
#&gt; SRR1927065     3  0.0767      0.963 0.000 0.008 0.976 0.000 0.012 0.004
#&gt; SRR1927067     3  0.1269      0.955 0.000 0.020 0.956 0.000 0.012 0.012
#&gt; SRR1927064     1  0.0717      0.963 0.976 0.000 0.000 0.008 0.000 0.016
#&gt; SRR1927063     3  0.1218      0.954 0.000 0.028 0.956 0.004 0.000 0.012
#&gt; SRR1927062     4  0.2972      0.823 0.128 0.000 0.000 0.836 0.000 0.036
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-5-a').click(function(){
  $('#tab-CV-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-CV-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-signatures'>
<ul>
<li><a href='#tab-CV-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-1-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-1"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-2-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-2"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-3-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-3"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-4-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-4"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-5-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-NMF-signature_compare](figure_cola/CV-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-CV-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-NMF-collect-classes](figure_cola/CV-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:hclust*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "hclust"]
# you can also extract it by
# res = res_list["MAD:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16868 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 5.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-hclust-collect-plots](figure_cola/MAD-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-hclust-select-partition-number](figure_cola/MAD-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5095 0.491   0.491
#> 3 3 0.755           0.950       0.931         0.2104 0.887   0.770
#> 4 4 0.907           0.946       0.959         0.2077 0.863   0.637
#> 5 5 0.917           0.930       0.956         0.0204 0.984   0.934
#> 6 6 0.979           0.918       0.973         0.0223 0.998   0.993
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 5
#> attr(,"optional")
#> [1] 2 4
```

There is also optional best $k$ = 2 4 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-classes'>
<ul>
<li><a href='#tab-MAD-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-hclust-get-classes-1'>
<p><a id='tab-MAD-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1927048     1       0          1  1  0
#&gt; SRR1927061     2       0          1  0  1
#&gt; SRR1927060     1       0          1  1  0
#&gt; SRR1927059     2       0          1  0  1
#&gt; SRR1927058     1       0          1  1  0
#&gt; SRR1927057     2       0          1  0  1
#&gt; SRR1927055     2       0          1  0  1
#&gt; SRR1927056     1       0          1  1  0
#&gt; SRR1927054     1       0          1  1  0
#&gt; SRR1927052     1       0          1  1  0
#&gt; SRR1927053     2       0          1  0  1
#&gt; SRR1927051     2       0          1  0  1
#&gt; SRR1927050     1       0          1  1  0
#&gt; SRR1927049     2       0          1  0  1
#&gt; SRR1927047     2       0          1  0  1
#&gt; SRR1927046     1       0          1  1  0
#&gt; SRR1927045     2       0          1  0  1
#&gt; SRR1927044     1       0          1  1  0
#&gt; SRR1927043     2       0          1  0  1
#&gt; SRR1927042     1       0          1  1  0
#&gt; SRR1927040     1       0          1  1  0
#&gt; SRR1927039     2       0          1  0  1
#&gt; SRR1927038     1       0          1  1  0
#&gt; SRR1927037     2       0          1  0  1
#&gt; SRR1927036     1       0          1  1  0
#&gt; SRR1927035     2       0          1  0  1
#&gt; SRR1927034     1       0          1  1  0
#&gt; SRR1927033     2       0          1  0  1
#&gt; SRR1927032     1       0          1  1  0
#&gt; SRR1927031     2       0          1  0  1
#&gt; SRR1927030     1       0          1  1  0
#&gt; SRR1927028     1       0          1  1  0
#&gt; SRR1927029     2       0          1  0  1
#&gt; SRR1927027     2       0          1  0  1
#&gt; SRR1927026     1       0          1  1  0
#&gt; SRR1927024     1       0          1  1  0
#&gt; SRR1927025     2       0          1  0  1
#&gt; SRR1927023     2       0          1  0  1
#&gt; SRR1927022     1       0          1  1  0
#&gt; SRR1927021     2       0          1  0  1
#&gt; SRR1927020     1       0          1  1  0
#&gt; SRR1927019     2       0          1  0  1
#&gt; SRR1927071     1       0          1  1  0
#&gt; SRR1927069     2       0          1  0  1
#&gt; SRR1927070     1       0          1  1  0
#&gt; SRR1927068     1       0          1  1  0
#&gt; SRR1927066     1       0          1  1  0
#&gt; SRR1927065     2       0          1  0  1
#&gt; SRR1927067     2       0          1  0  1
#&gt; SRR1927064     1       0          1  1  0
#&gt; SRR1927063     2       0          1  0  1
#&gt; SRR1927062     1       0          1  1  0
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-1-a').click(function(){
  $('#tab-MAD-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-2'>
<p><a id='tab-MAD-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1927048     1  0.0000      0.955 1.000 0.000 0.000
#&gt; SRR1927061     3  0.5497      0.888 0.000 0.292 0.708
#&gt; SRR1927060     1  0.0000      0.955 1.000 0.000 0.000
#&gt; SRR1927059     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1927058     1  0.0000      0.955 1.000 0.000 0.000
#&gt; SRR1927057     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1927055     3  0.3482      0.877 0.000 0.128 0.872
#&gt; SRR1927056     1  0.3482      0.933 0.872 0.000 0.128
#&gt; SRR1927054     1  0.0000      0.955 1.000 0.000 0.000
#&gt; SRR1927052     1  0.3038      0.942 0.896 0.000 0.104
#&gt; SRR1927053     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1927051     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1927050     1  0.3482      0.933 0.872 0.000 0.128
#&gt; SRR1927049     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1927047     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1927046     1  0.0000      0.955 1.000 0.000 0.000
#&gt; SRR1927045     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1927044     1  0.0000      0.955 1.000 0.000 0.000
#&gt; SRR1927043     3  0.5497      0.888 0.000 0.292 0.708
#&gt; SRR1927042     1  0.0000      0.955 1.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      0.955 1.000 0.000 0.000
#&gt; SRR1927039     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1927038     1  0.0000      0.955 1.000 0.000 0.000
#&gt; SRR1927037     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1927036     1  0.0000      0.955 1.000 0.000 0.000
#&gt; SRR1927035     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1927034     1  0.3482      0.933 0.872 0.000 0.128
#&gt; SRR1927033     3  0.3482      0.877 0.000 0.128 0.872
#&gt; SRR1927032     1  0.0000      0.955 1.000 0.000 0.000
#&gt; SRR1927031     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1927030     1  0.0000      0.955 1.000 0.000 0.000
#&gt; SRR1927028     1  0.3038      0.942 0.896 0.000 0.104
#&gt; SRR1927029     3  0.5497      0.888 0.000 0.292 0.708
#&gt; SRR1927027     3  0.3482      0.877 0.000 0.128 0.872
#&gt; SRR1927026     1  0.3038      0.942 0.896 0.000 0.104
#&gt; SRR1927024     1  0.3038      0.942 0.896 0.000 0.104
#&gt; SRR1927025     3  0.4796      0.888 0.000 0.220 0.780
#&gt; SRR1927023     3  0.3752      0.883 0.000 0.144 0.856
#&gt; SRR1927022     1  0.0424      0.954 0.992 0.000 0.008
#&gt; SRR1927021     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1927020     1  0.3482      0.933 0.872 0.000 0.128
#&gt; SRR1927019     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1927071     1  0.3038      0.942 0.896 0.000 0.104
#&gt; SRR1927069     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1927070     1  0.0000      0.955 1.000 0.000 0.000
#&gt; SRR1927068     1  0.3482      0.933 0.872 0.000 0.128
#&gt; SRR1927066     1  0.3038      0.942 0.896 0.000 0.104
#&gt; SRR1927065     3  0.5497      0.888 0.000 0.292 0.708
#&gt; SRR1927067     3  0.5497      0.888 0.000 0.292 0.708
#&gt; SRR1927064     1  0.0000      0.955 1.000 0.000 0.000
#&gt; SRR1927063     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1927062     1  0.3038      0.942 0.896 0.000 0.104
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-2-a').click(function(){
  $('#tab-MAD-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-3'>
<p><a id='tab-MAD-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1927048     1   0.000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927061     3   0.419      0.832 0.000 0.268 0.732 0.000
#&gt; SRR1927060     1   0.000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927059     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927058     1   0.000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927057     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927055     3   0.000      0.808 0.000 0.000 1.000 0.000
#&gt; SRR1927056     4   0.000      0.947 0.000 0.000 0.000 1.000
#&gt; SRR1927054     1   0.000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927052     4   0.102      0.955 0.032 0.000 0.000 0.968
#&gt; SRR1927053     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927051     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927050     4   0.000      0.947 0.000 0.000 0.000 1.000
#&gt; SRR1927049     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927047     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927046     1   0.000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927045     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927044     1   0.000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927043     3   0.413      0.839 0.000 0.260 0.740 0.000
#&gt; SRR1927042     1   0.000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927040     1   0.000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927039     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927038     1   0.000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927037     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927036     1   0.000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927035     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927034     4   0.000      0.947 0.000 0.000 0.000 1.000
#&gt; SRR1927033     3   0.000      0.808 0.000 0.000 1.000 0.000
#&gt; SRR1927032     1   0.000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927031     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927030     1   0.000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927028     4   0.102      0.955 0.032 0.000 0.000 0.968
#&gt; SRR1927029     3   0.413      0.839 0.000 0.260 0.740 0.000
#&gt; SRR1927027     3   0.000      0.808 0.000 0.000 1.000 0.000
#&gt; SRR1927026     4   0.102      0.955 0.032 0.000 0.000 0.968
#&gt; SRR1927024     4   0.102      0.955 0.032 0.000 0.000 0.968
#&gt; SRR1927025     3   0.365      0.833 0.000 0.204 0.796 0.000
#&gt; SRR1927023     3   0.147      0.828 0.000 0.052 0.948 0.000
#&gt; SRR1927022     4   0.464      0.514 0.344 0.000 0.000 0.656
#&gt; SRR1927021     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927020     4   0.000      0.947 0.000 0.000 0.000 1.000
#&gt; SRR1927019     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927071     4   0.102      0.955 0.032 0.000 0.000 0.968
#&gt; SRR1927069     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927070     1   0.000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927068     4   0.000      0.947 0.000 0.000 0.000 1.000
#&gt; SRR1927066     4   0.102      0.955 0.032 0.000 0.000 0.968
#&gt; SRR1927065     3   0.413      0.839 0.000 0.260 0.740 0.000
#&gt; SRR1927067     3   0.419      0.832 0.000 0.268 0.732 0.000
#&gt; SRR1927064     1   0.000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927063     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927062     4   0.102      0.955 0.032 0.000 0.000 0.968
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-3-a').click(function(){
  $('#tab-MAD-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-4'>
<p><a id='tab-MAD-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1927048     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927061     3  0.3480      0.851 0.000 0.248 0.752 0.000 0.000
#&gt; SRR1927060     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.0000      0.996 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927058     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927057     2  0.0000      0.996 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927055     3  0.0609      0.594 0.000 0.000 0.980 0.000 0.020
#&gt; SRR1927056     4  0.0000      0.937 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927054     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927052     4  0.0880      0.946 0.032 0.000 0.000 0.968 0.000
#&gt; SRR1927053     2  0.0000      0.996 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927051     2  0.0000      0.996 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927050     4  0.0000      0.937 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927049     2  0.0000      0.996 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927047     2  0.0000      0.996 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927046     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927045     2  0.0000      0.996 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927044     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927043     3  0.3424      0.857 0.000 0.240 0.760 0.000 0.000
#&gt; SRR1927042     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927039     2  0.0000      0.996 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927038     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.0000      0.996 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927036     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927035     2  0.0000      0.996 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927034     4  0.0000      0.937 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927033     3  0.0609      0.594 0.000 0.000 0.980 0.000 0.020
#&gt; SRR1927032     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927031     2  0.0000      0.996 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927030     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927028     4  0.0880      0.946 0.032 0.000 0.000 0.968 0.000
#&gt; SRR1927029     3  0.3424      0.857 0.000 0.240 0.760 0.000 0.000
#&gt; SRR1927027     5  0.3452      0.745 0.000 0.000 0.244 0.000 0.756
#&gt; SRR1927026     4  0.0880      0.946 0.032 0.000 0.000 0.968 0.000
#&gt; SRR1927024     4  0.0880      0.946 0.032 0.000 0.000 0.968 0.000
#&gt; SRR1927025     5  0.2690      0.705 0.000 0.156 0.000 0.000 0.844
#&gt; SRR1927023     5  0.0162      0.792 0.000 0.004 0.000 0.000 0.996
#&gt; SRR1927022     4  0.3999      0.489 0.344 0.000 0.000 0.656 0.000
#&gt; SRR1927021     2  0.1197      0.940 0.000 0.952 0.000 0.000 0.048
#&gt; SRR1927020     4  0.0000      0.937 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927019     2  0.0000      0.996 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927071     4  0.0880      0.946 0.032 0.000 0.000 0.968 0.000
#&gt; SRR1927069     2  0.0000      0.996 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927070     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927068     4  0.0000      0.937 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927066     4  0.0880      0.946 0.032 0.000 0.000 0.968 0.000
#&gt; SRR1927065     3  0.3424      0.857 0.000 0.240 0.760 0.000 0.000
#&gt; SRR1927067     3  0.3480      0.851 0.000 0.248 0.752 0.000 0.000
#&gt; SRR1927064     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927063     2  0.0000      0.996 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927062     4  0.0880      0.946 0.032 0.000 0.000 0.968 0.000
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-4-a').click(function(){
  $('#tab-MAD-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-5'>
<p><a id='tab-MAD-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1927048     1  0.0000      0.997 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927061     3  0.0692      0.897 0.000 0.020 0.976 0.000 0.000 0.004
#&gt; SRR1927060     1  0.0000      0.997 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927058     1  0.0000      0.997 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927057     2  0.0603      0.975 0.000 0.980 0.016 0.000 0.000 0.004
#&gt; SRR1927055     3  0.3101      0.704 0.000 0.000 0.756 0.000 0.000 0.244
#&gt; SRR1927056     4  0.0713      0.943 0.000 0.000 0.000 0.972 0.000 0.028
#&gt; SRR1927054     1  0.0000      0.997 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927052     4  0.0146      0.949 0.004 0.000 0.000 0.996 0.000 0.000
#&gt; SRR1927053     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927051     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927050     4  0.0713      0.943 0.000 0.000 0.000 0.972 0.000 0.028
#&gt; SRR1927049     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927047     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927046     1  0.0713      0.966 0.972 0.000 0.000 0.028 0.000 0.000
#&gt; SRR1927045     2  0.0363      0.983 0.000 0.988 0.012 0.000 0.000 0.000
#&gt; SRR1927044     1  0.0000      0.997 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927043     3  0.0458      0.899 0.000 0.016 0.984 0.000 0.000 0.000
#&gt; SRR1927042     1  0.0000      0.997 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      0.997 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927039     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927038     1  0.0000      0.997 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927036     1  0.0000      0.997 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927035     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927034     4  0.0713      0.943 0.000 0.000 0.000 0.972 0.000 0.028
#&gt; SRR1927033     3  0.3101      0.704 0.000 0.000 0.756 0.000 0.000 0.244
#&gt; SRR1927032     1  0.0000      0.997 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927031     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927030     1  0.0000      0.997 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927028     4  0.0146      0.949 0.004 0.000 0.000 0.996 0.000 0.000
#&gt; SRR1927029     3  0.0458      0.899 0.000 0.016 0.984 0.000 0.000 0.000
#&gt; SRR1927027     6  0.0914      0.000 0.000 0.000 0.016 0.000 0.016 0.968
#&gt; SRR1927026     4  0.0146      0.949 0.004 0.000 0.000 0.996 0.000 0.000
#&gt; SRR1927024     4  0.0146      0.949 0.004 0.000 0.000 0.996 0.000 0.000
#&gt; SRR1927025     5  0.2378      0.649 0.000 0.152 0.000 0.000 0.848 0.000
#&gt; SRR1927023     5  0.0000      0.626 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927022     4  0.3482      0.458 0.316 0.000 0.000 0.684 0.000 0.000
#&gt; SRR1927021     2  0.1141      0.941 0.000 0.948 0.000 0.000 0.052 0.000
#&gt; SRR1927020     4  0.0713      0.943 0.000 0.000 0.000 0.972 0.000 0.028
#&gt; SRR1927019     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927071     4  0.0146      0.949 0.004 0.000 0.000 0.996 0.000 0.000
#&gt; SRR1927069     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927070     1  0.0000      0.997 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927068     4  0.0713      0.943 0.000 0.000 0.000 0.972 0.000 0.028
#&gt; SRR1927066     4  0.0146      0.949 0.004 0.000 0.000 0.996 0.000 0.000
#&gt; SRR1927065     3  0.0458      0.899 0.000 0.016 0.984 0.000 0.000 0.000
#&gt; SRR1927067     3  0.0692      0.897 0.000 0.020 0.976 0.000 0.000 0.004
#&gt; SRR1927064     1  0.0000      0.997 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927063     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927062     4  0.0146      0.949 0.004 0.000 0.000 0.996 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-5-a').click(function(){
  $('#tab-MAD-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-signatures'>
<ul>
<li><a href='#tab-MAD-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-1-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-1"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-2-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-2"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-3-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-3"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-4-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-4"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-5-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-hclust-signature_compare](figure_cola/MAD-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-hclust-collect-classes](figure_cola/MAD-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:kmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "kmeans"]
# you can also extract it by
# res = res_list["MAD:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16868 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-kmeans-collect-plots](figure_cola/MAD-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-kmeans-select-partition-number](figure_cola/MAD-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5095 0.491   0.491
#> 3 3 0.746           0.857       0.801         0.2494 0.864   0.724
#> 4 4 0.697           0.893       0.858         0.1288 0.872   0.648
#> 5 5 0.630           0.743       0.828         0.0647 0.994   0.975
#> 6 6 0.811           0.745       0.780         0.0494 0.964   0.849
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-classes'>
<ul>
<li><a href='#tab-MAD-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-kmeans-get-classes-1'>
<p><a id='tab-MAD-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1927048     1       0          1  1  0
#&gt; SRR1927061     2       0          1  0  1
#&gt; SRR1927060     1       0          1  1  0
#&gt; SRR1927059     2       0          1  0  1
#&gt; SRR1927058     1       0          1  1  0
#&gt; SRR1927057     2       0          1  0  1
#&gt; SRR1927055     2       0          1  0  1
#&gt; SRR1927056     1       0          1  1  0
#&gt; SRR1927054     1       0          1  1  0
#&gt; SRR1927052     1       0          1  1  0
#&gt; SRR1927053     2       0          1  0  1
#&gt; SRR1927051     2       0          1  0  1
#&gt; SRR1927050     1       0          1  1  0
#&gt; SRR1927049     2       0          1  0  1
#&gt; SRR1927047     2       0          1  0  1
#&gt; SRR1927046     1       0          1  1  0
#&gt; SRR1927045     2       0          1  0  1
#&gt; SRR1927044     1       0          1  1  0
#&gt; SRR1927043     2       0          1  0  1
#&gt; SRR1927042     1       0          1  1  0
#&gt; SRR1927040     1       0          1  1  0
#&gt; SRR1927039     2       0          1  0  1
#&gt; SRR1927038     1       0          1  1  0
#&gt; SRR1927037     2       0          1  0  1
#&gt; SRR1927036     1       0          1  1  0
#&gt; SRR1927035     2       0          1  0  1
#&gt; SRR1927034     1       0          1  1  0
#&gt; SRR1927033     2       0          1  0  1
#&gt; SRR1927032     1       0          1  1  0
#&gt; SRR1927031     2       0          1  0  1
#&gt; SRR1927030     1       0          1  1  0
#&gt; SRR1927028     1       0          1  1  0
#&gt; SRR1927029     2       0          1  0  1
#&gt; SRR1927027     2       0          1  0  1
#&gt; SRR1927026     1       0          1  1  0
#&gt; SRR1927024     1       0          1  1  0
#&gt; SRR1927025     2       0          1  0  1
#&gt; SRR1927023     2       0          1  0  1
#&gt; SRR1927022     1       0          1  1  0
#&gt; SRR1927021     2       0          1  0  1
#&gt; SRR1927020     1       0          1  1  0
#&gt; SRR1927019     2       0          1  0  1
#&gt; SRR1927071     1       0          1  1  0
#&gt; SRR1927069     2       0          1  0  1
#&gt; SRR1927070     1       0          1  1  0
#&gt; SRR1927068     1       0          1  1  0
#&gt; SRR1927066     1       0          1  1  0
#&gt; SRR1927065     2       0          1  0  1
#&gt; SRR1927067     2       0          1  0  1
#&gt; SRR1927064     1       0          1  1  0
#&gt; SRR1927063     2       0          1  0  1
#&gt; SRR1927062     1       0          1  1  0
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-1-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-2'>
<p><a id='tab-MAD-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1927048     1  0.0000      0.954 1.000 0.000 0.000
#&gt; SRR1927061     2  0.0237      0.726 0.000 0.996 0.004
#&gt; SRR1927060     1  0.0000      0.954 1.000 0.000 0.000
#&gt; SRR1927059     2  0.6267      0.843 0.000 0.548 0.452
#&gt; SRR1927058     1  0.0000      0.954 1.000 0.000 0.000
#&gt; SRR1927057     2  0.6267      0.843 0.000 0.548 0.452
#&gt; SRR1927055     2  0.0000      0.725 0.000 1.000 0.000
#&gt; SRR1927056     3  0.6267      1.000 0.452 0.000 0.548
#&gt; SRR1927054     1  0.0000      0.954 1.000 0.000 0.000
#&gt; SRR1927052     3  0.6267      1.000 0.452 0.000 0.548
#&gt; SRR1927053     2  0.6267      0.843 0.000 0.548 0.452
#&gt; SRR1927051     2  0.6267      0.843 0.000 0.548 0.452
#&gt; SRR1927050     3  0.6267      1.000 0.452 0.000 0.548
#&gt; SRR1927049     2  0.6267      0.843 0.000 0.548 0.452
#&gt; SRR1927047     2  0.6267      0.843 0.000 0.548 0.452
#&gt; SRR1927046     1  0.0000      0.954 1.000 0.000 0.000
#&gt; SRR1927045     2  0.6267      0.843 0.000 0.548 0.452
#&gt; SRR1927044     1  0.0000      0.954 1.000 0.000 0.000
#&gt; SRR1927043     2  0.0000      0.725 0.000 1.000 0.000
#&gt; SRR1927042     1  0.0000      0.954 1.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      0.954 1.000 0.000 0.000
#&gt; SRR1927039     2  0.6267      0.843 0.000 0.548 0.452
#&gt; SRR1927038     1  0.0000      0.954 1.000 0.000 0.000
#&gt; SRR1927037     2  0.6267      0.843 0.000 0.548 0.452
#&gt; SRR1927036     1  0.0000      0.954 1.000 0.000 0.000
#&gt; SRR1927035     2  0.6267      0.843 0.000 0.548 0.452
#&gt; SRR1927034     3  0.6267      1.000 0.452 0.000 0.548
#&gt; SRR1927033     2  0.0000      0.725 0.000 1.000 0.000
#&gt; SRR1927032     1  0.0000      0.954 1.000 0.000 0.000
#&gt; SRR1927031     2  0.6267      0.843 0.000 0.548 0.452
#&gt; SRR1927030     1  0.0000      0.954 1.000 0.000 0.000
#&gt; SRR1927028     3  0.6267      1.000 0.452 0.000 0.548
#&gt; SRR1927029     2  0.0000      0.725 0.000 1.000 0.000
#&gt; SRR1927027     2  0.5098      0.403 0.000 0.752 0.248
#&gt; SRR1927026     3  0.6267      1.000 0.452 0.000 0.548
#&gt; SRR1927024     3  0.6267      1.000 0.452 0.000 0.548
#&gt; SRR1927025     2  0.3941      0.771 0.000 0.844 0.156
#&gt; SRR1927023     2  0.1643      0.739 0.000 0.956 0.044
#&gt; SRR1927022     1  0.5882     -0.421 0.652 0.000 0.348
#&gt; SRR1927021     2  0.6267      0.843 0.000 0.548 0.452
#&gt; SRR1927020     3  0.6267      1.000 0.452 0.000 0.548
#&gt; SRR1927019     2  0.6267      0.843 0.000 0.548 0.452
#&gt; SRR1927071     3  0.6267      1.000 0.452 0.000 0.548
#&gt; SRR1927069     2  0.6267      0.843 0.000 0.548 0.452
#&gt; SRR1927070     1  0.0000      0.954 1.000 0.000 0.000
#&gt; SRR1927068     3  0.6267      1.000 0.452 0.000 0.548
#&gt; SRR1927066     3  0.6267      1.000 0.452 0.000 0.548
#&gt; SRR1927065     2  0.0000      0.725 0.000 1.000 0.000
#&gt; SRR1927067     2  0.0000      0.725 0.000 1.000 0.000
#&gt; SRR1927064     1  0.0000      0.954 1.000 0.000 0.000
#&gt; SRR1927063     2  0.6267      0.843 0.000 0.548 0.452
#&gt; SRR1927062     3  0.6267      1.000 0.452 0.000 0.548
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-2-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-3'>
<p><a id='tab-MAD-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1927048     1  0.4323      0.955 0.788 0.000 0.028 0.184
#&gt; SRR1927061     3  0.4401      0.893 0.004 0.272 0.724 0.000
#&gt; SRR1927060     1  0.4508      0.957 0.780 0.000 0.036 0.184
#&gt; SRR1927059     2  0.0336      0.942 0.008 0.992 0.000 0.000
#&gt; SRR1927058     1  0.4508      0.957 0.780 0.000 0.036 0.184
#&gt; SRR1927057     2  0.0469      0.942 0.012 0.988 0.000 0.000
#&gt; SRR1927055     3  0.6064      0.860 0.108 0.220 0.672 0.000
#&gt; SRR1927056     4  0.2921      0.902 0.000 0.000 0.140 0.860
#&gt; SRR1927054     1  0.4508      0.957 0.780 0.000 0.036 0.184
#&gt; SRR1927052     4  0.1557      0.894 0.000 0.000 0.056 0.944
#&gt; SRR1927053     2  0.0336      0.942 0.008 0.992 0.000 0.000
#&gt; SRR1927051     2  0.0188      0.942 0.004 0.996 0.000 0.000
#&gt; SRR1927050     4  0.2921      0.902 0.000 0.000 0.140 0.860
#&gt; SRR1927049     2  0.0188      0.942 0.004 0.996 0.000 0.000
#&gt; SRR1927047     2  0.0336      0.942 0.008 0.992 0.000 0.000
#&gt; SRR1927046     1  0.5200      0.942 0.744 0.000 0.072 0.184
#&gt; SRR1927045     2  0.1978      0.864 0.004 0.928 0.068 0.000
#&gt; SRR1927044     1  0.5062      0.946 0.752 0.000 0.064 0.184
#&gt; SRR1927043     3  0.4134      0.904 0.000 0.260 0.740 0.000
#&gt; SRR1927042     1  0.3444      0.959 0.816 0.000 0.000 0.184
#&gt; SRR1927040     1  0.4508      0.957 0.780 0.000 0.036 0.184
#&gt; SRR1927039     2  0.0336      0.942 0.008 0.992 0.000 0.000
#&gt; SRR1927038     1  0.4508      0.957 0.780 0.000 0.036 0.184
#&gt; SRR1927037     2  0.0336      0.942 0.008 0.992 0.000 0.000
#&gt; SRR1927036     1  0.4916      0.946 0.760 0.000 0.056 0.184
#&gt; SRR1927035     2  0.0000      0.942 0.000 1.000 0.000 0.000
#&gt; SRR1927034     4  0.2921      0.902 0.000 0.000 0.140 0.860
#&gt; SRR1927033     3  0.6352      0.876 0.108 0.260 0.632 0.000
#&gt; SRR1927032     1  0.4679      0.956 0.772 0.000 0.044 0.184
#&gt; SRR1927031     2  0.0336      0.942 0.008 0.992 0.000 0.000
#&gt; SRR1927030     1  0.4916      0.946 0.760 0.000 0.056 0.184
#&gt; SRR1927028     4  0.0000      0.926 0.000 0.000 0.000 1.000
#&gt; SRR1927029     3  0.4134      0.904 0.000 0.260 0.740 0.000
#&gt; SRR1927027     3  0.7062      0.727 0.160 0.108 0.668 0.064
#&gt; SRR1927026     4  0.0000      0.926 0.000 0.000 0.000 1.000
#&gt; SRR1927024     4  0.0000      0.926 0.000 0.000 0.000 1.000
#&gt; SRR1927025     2  0.6384     -0.458 0.064 0.496 0.440 0.000
#&gt; SRR1927023     3  0.7282      0.792 0.172 0.316 0.512 0.000
#&gt; SRR1927022     4  0.3732      0.794 0.092 0.000 0.056 0.852
#&gt; SRR1927021     2  0.0469      0.935 0.012 0.988 0.000 0.000
#&gt; SRR1927020     4  0.2921      0.902 0.000 0.000 0.140 0.860
#&gt; SRR1927019     2  0.0188      0.942 0.004 0.996 0.000 0.000
#&gt; SRR1927071     4  0.0000      0.926 0.000 0.000 0.000 1.000
#&gt; SRR1927069     2  0.0000      0.942 0.000 1.000 0.000 0.000
#&gt; SRR1927070     1  0.4916      0.946 0.760 0.000 0.056 0.184
#&gt; SRR1927068     4  0.2921      0.902 0.000 0.000 0.140 0.860
#&gt; SRR1927066     4  0.0188      0.925 0.000 0.000 0.004 0.996
#&gt; SRR1927065     3  0.4134      0.904 0.000 0.260 0.740 0.000
#&gt; SRR1927067     3  0.4134      0.904 0.000 0.260 0.740 0.000
#&gt; SRR1927064     1  0.4323      0.955 0.788 0.000 0.028 0.184
#&gt; SRR1927063     2  0.0188      0.942 0.004 0.996 0.000 0.000
#&gt; SRR1927062     4  0.0188      0.925 0.000 0.000 0.004 0.996
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-3-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-4'>
<p><a id='tab-MAD-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1927048     1  0.1701      0.879 0.936 0.000 0.016 0.000 0.048
#&gt; SRR1927061     3  0.2909      0.647 0.000 0.140 0.848 0.012 0.000
#&gt; SRR1927060     1  0.3239      0.855 0.852 0.000 0.080 0.000 0.068
#&gt; SRR1927059     2  0.2171      0.889 0.000 0.912 0.000 0.064 0.024
#&gt; SRR1927058     1  0.1915      0.878 0.928 0.000 0.040 0.000 0.032
#&gt; SRR1927057     2  0.1877      0.895 0.000 0.924 0.000 0.064 0.012
#&gt; SRR1927055     3  0.5334      0.218 0.000 0.104 0.652 0.000 0.244
#&gt; SRR1927056     4  0.5606      0.794 0.104 0.000 0.000 0.600 0.296
#&gt; SRR1927054     1  0.3239      0.855 0.852 0.000 0.080 0.000 0.068
#&gt; SRR1927052     4  0.4316      0.780 0.108 0.000 0.000 0.772 0.120
#&gt; SRR1927053     2  0.2171      0.889 0.000 0.912 0.000 0.064 0.024
#&gt; SRR1927051     2  0.0290      0.899 0.000 0.992 0.000 0.008 0.000
#&gt; SRR1927050     4  0.5606      0.794 0.104 0.000 0.000 0.600 0.296
#&gt; SRR1927049     2  0.0510      0.897 0.000 0.984 0.000 0.016 0.000
#&gt; SRR1927047     2  0.1386      0.899 0.000 0.952 0.000 0.032 0.016
#&gt; SRR1927046     1  0.3081      0.849 0.832 0.000 0.012 0.000 0.156
#&gt; SRR1927045     2  0.2233      0.826 0.000 0.904 0.080 0.016 0.000
#&gt; SRR1927044     1  0.2953      0.851 0.844 0.000 0.012 0.000 0.144
#&gt; SRR1927043     3  0.2329      0.680 0.000 0.124 0.876 0.000 0.000
#&gt; SRR1927042     1  0.0000      0.884 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.3239      0.855 0.852 0.000 0.080 0.000 0.068
#&gt; SRR1927039     2  0.2171      0.889 0.000 0.912 0.000 0.064 0.024
#&gt; SRR1927038     1  0.3239      0.855 0.852 0.000 0.080 0.000 0.068
#&gt; SRR1927037     2  0.2036      0.891 0.000 0.920 0.000 0.056 0.024
#&gt; SRR1927036     1  0.2886      0.849 0.844 0.000 0.008 0.000 0.148
#&gt; SRR1927035     2  0.0162      0.899 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1927034     4  0.5606      0.794 0.104 0.000 0.000 0.600 0.296
#&gt; SRR1927033     3  0.5423      0.242 0.000 0.124 0.652 0.000 0.224
#&gt; SRR1927032     1  0.2291      0.878 0.908 0.000 0.036 0.000 0.056
#&gt; SRR1927031     2  0.1893      0.893 0.000 0.928 0.000 0.048 0.024
#&gt; SRR1927030     1  0.2886      0.849 0.844 0.000 0.008 0.000 0.148
#&gt; SRR1927028     4  0.2074      0.845 0.104 0.000 0.000 0.896 0.000
#&gt; SRR1927029     3  0.2329      0.680 0.000 0.124 0.876 0.000 0.000
#&gt; SRR1927027     3  0.5602     -0.490 0.000 0.060 0.472 0.004 0.464
#&gt; SRR1927026     4  0.2669      0.846 0.104 0.000 0.020 0.876 0.000
#&gt; SRR1927024     4  0.2669      0.846 0.104 0.000 0.020 0.876 0.000
#&gt; SRR1927025     2  0.7192     -0.540 0.000 0.412 0.368 0.032 0.188
#&gt; SRR1927023     5  0.6917      0.000 0.000 0.172 0.396 0.020 0.412
#&gt; SRR1927022     4  0.6179      0.636 0.196 0.000 0.028 0.628 0.148
#&gt; SRR1927021     2  0.1493      0.881 0.000 0.948 0.000 0.024 0.028
#&gt; SRR1927020     4  0.5606      0.794 0.104 0.000 0.000 0.600 0.296
#&gt; SRR1927019     2  0.0404      0.898 0.000 0.988 0.000 0.012 0.000
#&gt; SRR1927071     4  0.2074      0.845 0.104 0.000 0.000 0.896 0.000
#&gt; SRR1927069     2  0.0510      0.899 0.000 0.984 0.000 0.016 0.000
#&gt; SRR1927070     1  0.2886      0.849 0.844 0.000 0.008 0.000 0.148
#&gt; SRR1927068     4  0.5606      0.794 0.104 0.000 0.000 0.600 0.296
#&gt; SRR1927066     4  0.2848      0.840 0.104 0.000 0.000 0.868 0.028
#&gt; SRR1927065     3  0.2707      0.665 0.000 0.132 0.860 0.008 0.000
#&gt; SRR1927067     3  0.2329      0.680 0.000 0.124 0.876 0.000 0.000
#&gt; SRR1927064     1  0.1386      0.879 0.952 0.000 0.016 0.000 0.032
#&gt; SRR1927063     2  0.0510      0.898 0.000 0.984 0.000 0.016 0.000
#&gt; SRR1927062     4  0.2848      0.840 0.104 0.000 0.000 0.868 0.028
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-4-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-5'>
<p><a id='tab-MAD-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1927048     1  0.4024      0.798 0.748 0.000 0.008 0.048 0.196 0.000
#&gt; SRR1927061     3  0.1843      0.709 0.000 0.080 0.912 0.004 0.000 0.004
#&gt; SRR1927060     1  0.2933      0.757 0.860 0.000 0.032 0.016 0.092 0.000
#&gt; SRR1927059     2  0.3213      0.823 0.000 0.808 0.000 0.160 0.032 0.000
#&gt; SRR1927058     1  0.1141      0.794 0.948 0.000 0.000 0.000 0.052 0.000
#&gt; SRR1927057     2  0.2845      0.833 0.000 0.836 0.000 0.148 0.008 0.008
#&gt; SRR1927055     3  0.4675     -0.130 0.000 0.044 0.592 0.000 0.360 0.004
#&gt; SRR1927056     6  0.1007      0.985 0.044 0.000 0.000 0.000 0.000 0.956
#&gt; SRR1927054     1  0.2933      0.757 0.860 0.000 0.032 0.016 0.092 0.000
#&gt; SRR1927052     4  0.4506      0.737 0.044 0.000 0.000 0.608 0.000 0.348
#&gt; SRR1927053     2  0.3213      0.823 0.000 0.808 0.000 0.160 0.032 0.000
#&gt; SRR1927051     2  0.0865      0.847 0.000 0.964 0.000 0.036 0.000 0.000
#&gt; SRR1927050     6  0.1523      0.979 0.044 0.000 0.000 0.008 0.008 0.940
#&gt; SRR1927049     2  0.0937      0.846 0.000 0.960 0.000 0.040 0.000 0.000
#&gt; SRR1927047     2  0.1908      0.848 0.000 0.916 0.000 0.056 0.028 0.000
#&gt; SRR1927046     1  0.4845      0.781 0.660 0.000 0.000 0.132 0.208 0.000
#&gt; SRR1927045     2  0.2488      0.793 0.000 0.880 0.076 0.044 0.000 0.000
#&gt; SRR1927044     1  0.4757      0.779 0.676 0.000 0.000 0.180 0.144 0.000
#&gt; SRR1927043     3  0.1075      0.742 0.000 0.048 0.952 0.000 0.000 0.000
#&gt; SRR1927042     1  0.2999      0.813 0.840 0.000 0.000 0.048 0.112 0.000
#&gt; SRR1927040     1  0.2933      0.757 0.860 0.000 0.032 0.016 0.092 0.000
#&gt; SRR1927039     2  0.3213      0.823 0.000 0.808 0.000 0.160 0.032 0.000
#&gt; SRR1927038     1  0.2933      0.757 0.860 0.000 0.032 0.016 0.092 0.000
#&gt; SRR1927037     2  0.3102      0.825 0.000 0.816 0.000 0.156 0.028 0.000
#&gt; SRR1927036     1  0.4752      0.779 0.676 0.000 0.000 0.184 0.140 0.000
#&gt; SRR1927035     2  0.0790      0.848 0.000 0.968 0.000 0.032 0.000 0.000
#&gt; SRR1927034     6  0.1523      0.979 0.044 0.000 0.000 0.008 0.008 0.940
#&gt; SRR1927033     3  0.4598     -0.119 0.000 0.048 0.592 0.000 0.360 0.000
#&gt; SRR1927032     1  0.2325      0.791 0.884 0.000 0.008 0.008 0.100 0.000
#&gt; SRR1927031     2  0.3050      0.829 0.000 0.832 0.000 0.136 0.028 0.004
#&gt; SRR1927030     1  0.4752      0.779 0.676 0.000 0.000 0.184 0.140 0.000
#&gt; SRR1927028     4  0.4834      0.831 0.044 0.000 0.000 0.480 0.004 0.472
#&gt; SRR1927029     3  0.1075      0.742 0.000 0.048 0.952 0.000 0.000 0.000
#&gt; SRR1927027     5  0.4860      0.601 0.000 0.032 0.400 0.000 0.552 0.016
#&gt; SRR1927026     4  0.5396      0.824 0.044 0.000 0.008 0.464 0.020 0.464
#&gt; SRR1927024     4  0.5396      0.824 0.044 0.000 0.008 0.464 0.020 0.464
#&gt; SRR1927025     2  0.8041     -0.498 0.000 0.320 0.304 0.120 0.216 0.040
#&gt; SRR1927023     5  0.7071      0.648 0.000 0.080 0.340 0.092 0.452 0.036
#&gt; SRR1927022     4  0.5847      0.515 0.100 0.000 0.008 0.612 0.044 0.236
#&gt; SRR1927021     2  0.2302      0.821 0.000 0.900 0.000 0.060 0.032 0.008
#&gt; SRR1927020     6  0.1152      0.984 0.044 0.000 0.000 0.000 0.004 0.952
#&gt; SRR1927019     2  0.0291      0.852 0.000 0.992 0.000 0.004 0.000 0.004
#&gt; SRR1927071     4  0.4834      0.831 0.044 0.000 0.000 0.480 0.004 0.472
#&gt; SRR1927069     2  0.1219      0.848 0.000 0.948 0.000 0.048 0.004 0.000
#&gt; SRR1927070     1  0.4752      0.779 0.676 0.000 0.000 0.184 0.140 0.000
#&gt; SRR1927068     6  0.1152      0.984 0.044 0.000 0.000 0.000 0.004 0.952
#&gt; SRR1927066     4  0.4689      0.835 0.044 0.000 0.000 0.516 0.000 0.440
#&gt; SRR1927065     3  0.1674      0.724 0.000 0.068 0.924 0.004 0.000 0.004
#&gt; SRR1927067     3  0.1075      0.742 0.000 0.048 0.952 0.000 0.000 0.000
#&gt; SRR1927064     1  0.3867      0.798 0.760 0.000 0.008 0.040 0.192 0.000
#&gt; SRR1927063     2  0.0508      0.852 0.000 0.984 0.000 0.012 0.000 0.004
#&gt; SRR1927062     4  0.4825      0.831 0.044 0.000 0.000 0.504 0.004 0.448
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-5-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-signatures'>
<ul>
<li><a href='#tab-MAD-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-kmeans-signature_compare](figure_cola/MAD-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-kmeans-collect-classes](figure_cola/MAD-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:skmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "skmeans"]
# you can also extract it by
# res = res_list["MAD:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16868 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 5.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-skmeans-collect-plots](figure_cola/MAD-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-skmeans-select-partition-number](figure_cola/MAD-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5095 0.491   0.491
#> 3 3 1.000           0.968       0.982         0.2741 0.863   0.720
#> 4 4 1.000           0.967       0.986         0.1627 0.891   0.693
#> 5 5 1.000           0.966       0.982         0.0259 0.977   0.905
#> 6 6 0.896           0.871       0.915         0.0264 0.989   0.953
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 5
#> attr(,"optional")
#> [1] 2 3 4
```

There is also optional best $k$ = 2 3 4 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-classes'>
<ul>
<li><a href='#tab-MAD-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-skmeans-get-classes-1'>
<p><a id='tab-MAD-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1927048     1       0          1  1  0
#&gt; SRR1927061     2       0          1  0  1
#&gt; SRR1927060     1       0          1  1  0
#&gt; SRR1927059     2       0          1  0  1
#&gt; SRR1927058     1       0          1  1  0
#&gt; SRR1927057     2       0          1  0  1
#&gt; SRR1927055     2       0          1  0  1
#&gt; SRR1927056     1       0          1  1  0
#&gt; SRR1927054     1       0          1  1  0
#&gt; SRR1927052     1       0          1  1  0
#&gt; SRR1927053     2       0          1  0  1
#&gt; SRR1927051     2       0          1  0  1
#&gt; SRR1927050     1       0          1  1  0
#&gt; SRR1927049     2       0          1  0  1
#&gt; SRR1927047     2       0          1  0  1
#&gt; SRR1927046     1       0          1  1  0
#&gt; SRR1927045     2       0          1  0  1
#&gt; SRR1927044     1       0          1  1  0
#&gt; SRR1927043     2       0          1  0  1
#&gt; SRR1927042     1       0          1  1  0
#&gt; SRR1927040     1       0          1  1  0
#&gt; SRR1927039     2       0          1  0  1
#&gt; SRR1927038     1       0          1  1  0
#&gt; SRR1927037     2       0          1  0  1
#&gt; SRR1927036     1       0          1  1  0
#&gt; SRR1927035     2       0          1  0  1
#&gt; SRR1927034     1       0          1  1  0
#&gt; SRR1927033     2       0          1  0  1
#&gt; SRR1927032     1       0          1  1  0
#&gt; SRR1927031     2       0          1  0  1
#&gt; SRR1927030     1       0          1  1  0
#&gt; SRR1927028     1       0          1  1  0
#&gt; SRR1927029     2       0          1  0  1
#&gt; SRR1927027     2       0          1  0  1
#&gt; SRR1927026     1       0          1  1  0
#&gt; SRR1927024     1       0          1  1  0
#&gt; SRR1927025     2       0          1  0  1
#&gt; SRR1927023     2       0          1  0  1
#&gt; SRR1927022     1       0          1  1  0
#&gt; SRR1927021     2       0          1  0  1
#&gt; SRR1927020     1       0          1  1  0
#&gt; SRR1927019     2       0          1  0  1
#&gt; SRR1927071     1       0          1  1  0
#&gt; SRR1927069     2       0          1  0  1
#&gt; SRR1927070     1       0          1  1  0
#&gt; SRR1927068     1       0          1  1  0
#&gt; SRR1927066     1       0          1  1  0
#&gt; SRR1927065     2       0          1  0  1
#&gt; SRR1927067     2       0          1  0  1
#&gt; SRR1927064     1       0          1  1  0
#&gt; SRR1927063     2       0          1  0  1
#&gt; SRR1927062     1       0          1  1  0
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-1-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-2'>
<p><a id='tab-MAD-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1927048     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927061     2  0.0747      0.974 0.000 0.984 0.016
#&gt; SRR1927060     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927059     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927058     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927057     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927055     2  0.0747      0.974 0.000 0.984 0.016
#&gt; SRR1927056     3  0.0747      0.984 0.016 0.000 0.984
#&gt; SRR1927054     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927052     3  0.0747      0.984 0.016 0.000 0.984
#&gt; SRR1927053     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927051     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927050     3  0.0747      0.984 0.016 0.000 0.984
#&gt; SRR1927049     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927047     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927046     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927045     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927044     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927043     2  0.0747      0.974 0.000 0.984 0.016
#&gt; SRR1927042     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927039     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927038     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927037     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927036     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927035     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927034     3  0.0747      0.984 0.016 0.000 0.984
#&gt; SRR1927033     2  0.0747      0.974 0.000 0.984 0.016
#&gt; SRR1927032     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927031     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927030     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927028     3  0.0747      0.984 0.016 0.000 0.984
#&gt; SRR1927029     2  0.0747      0.974 0.000 0.984 0.016
#&gt; SRR1927027     2  0.6168      0.325 0.000 0.588 0.412
#&gt; SRR1927026     3  0.0747      0.984 0.016 0.000 0.984
#&gt; SRR1927024     3  0.0747      0.984 0.016 0.000 0.984
#&gt; SRR1927025     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927023     2  0.0747      0.974 0.000 0.984 0.016
#&gt; SRR1927022     3  0.4605      0.765 0.204 0.000 0.796
#&gt; SRR1927021     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927020     3  0.0747      0.984 0.016 0.000 0.984
#&gt; SRR1927019     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927071     3  0.0747      0.984 0.016 0.000 0.984
#&gt; SRR1927069     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927070     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927068     3  0.0747      0.984 0.016 0.000 0.984
#&gt; SRR1927066     3  0.0747      0.984 0.016 0.000 0.984
#&gt; SRR1927065     2  0.0747      0.974 0.000 0.984 0.016
#&gt; SRR1927067     2  0.0747      0.974 0.000 0.984 0.016
#&gt; SRR1927064     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1927063     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927062     3  0.0747      0.984 0.016 0.000 0.984
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-2-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-3'>
<p><a id='tab-MAD-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1927048     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927061     3  0.0188      0.973 0.000 0.004 0.996 0.000
#&gt; SRR1927060     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.0000      0.978 0.000 1.000 0.000 0.000
#&gt; SRR1927058     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927057     2  0.0000      0.978 0.000 1.000 0.000 0.000
#&gt; SRR1927055     3  0.0188      0.973 0.000 0.004 0.996 0.000
#&gt; SRR1927056     4  0.0188      0.981 0.000 0.000 0.004 0.996
#&gt; SRR1927054     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927052     4  0.0000      0.981 0.000 0.000 0.000 1.000
#&gt; SRR1927053     2  0.0000      0.978 0.000 1.000 0.000 0.000
#&gt; SRR1927051     2  0.0000      0.978 0.000 1.000 0.000 0.000
#&gt; SRR1927050     4  0.0188      0.981 0.000 0.000 0.004 0.996
#&gt; SRR1927049     2  0.0000      0.978 0.000 1.000 0.000 0.000
#&gt; SRR1927047     2  0.0000      0.978 0.000 1.000 0.000 0.000
#&gt; SRR1927046     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927045     2  0.0000      0.978 0.000 1.000 0.000 0.000
#&gt; SRR1927044     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927043     3  0.0188      0.973 0.000 0.004 0.996 0.000
#&gt; SRR1927042     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927039     2  0.0000      0.978 0.000 1.000 0.000 0.000
#&gt; SRR1927038     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.0000      0.978 0.000 1.000 0.000 0.000
#&gt; SRR1927036     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927035     2  0.0000      0.978 0.000 1.000 0.000 0.000
#&gt; SRR1927034     4  0.0188      0.981 0.000 0.000 0.004 0.996
#&gt; SRR1927033     3  0.0188      0.973 0.000 0.004 0.996 0.000
#&gt; SRR1927032     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927031     2  0.0000      0.978 0.000 1.000 0.000 0.000
#&gt; SRR1927030     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927028     4  0.0000      0.981 0.000 0.000 0.000 1.000
#&gt; SRR1927029     3  0.0188      0.973 0.000 0.004 0.996 0.000
#&gt; SRR1927027     3  0.0188      0.973 0.000 0.004 0.996 0.000
#&gt; SRR1927026     4  0.0000      0.981 0.000 0.000 0.000 1.000
#&gt; SRR1927024     4  0.0000      0.981 0.000 0.000 0.000 1.000
#&gt; SRR1927025     2  0.4477      0.522 0.000 0.688 0.312 0.000
#&gt; SRR1927023     3  0.3610      0.744 0.000 0.200 0.800 0.000
#&gt; SRR1927022     4  0.3444      0.774 0.184 0.000 0.000 0.816
#&gt; SRR1927021     2  0.0000      0.978 0.000 1.000 0.000 0.000
#&gt; SRR1927020     4  0.0188      0.981 0.000 0.000 0.004 0.996
#&gt; SRR1927019     2  0.0000      0.978 0.000 1.000 0.000 0.000
#&gt; SRR1927071     4  0.0000      0.981 0.000 0.000 0.000 1.000
#&gt; SRR1927069     2  0.0000      0.978 0.000 1.000 0.000 0.000
#&gt; SRR1927070     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927068     4  0.0188      0.981 0.000 0.000 0.004 0.996
#&gt; SRR1927066     4  0.0000      0.981 0.000 0.000 0.000 1.000
#&gt; SRR1927065     3  0.0188      0.973 0.000 0.004 0.996 0.000
#&gt; SRR1927067     3  0.0188      0.973 0.000 0.004 0.996 0.000
#&gt; SRR1927064     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927063     2  0.0000      0.978 0.000 1.000 0.000 0.000
#&gt; SRR1927062     4  0.0000      0.981 0.000 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-3-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-4'>
<p><a id='tab-MAD-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1927048     1  0.0000      0.987 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927061     3  0.0000      0.990 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927060     1  0.0000      0.987 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927058     1  0.0000      0.987 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927057     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927055     3  0.0794      0.976 0.000 0.000 0.972 0.000 0.028
#&gt; SRR1927056     4  0.0609      0.968 0.000 0.000 0.000 0.980 0.020
#&gt; SRR1927054     1  0.0000      0.987 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927052     4  0.0290      0.966 0.000 0.000 0.000 0.992 0.008
#&gt; SRR1927053     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927051     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927050     4  0.0609      0.968 0.000 0.000 0.000 0.980 0.020
#&gt; SRR1927049     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927047     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927046     1  0.0963      0.976 0.964 0.000 0.000 0.000 0.036
#&gt; SRR1927045     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927044     1  0.0963      0.976 0.964 0.000 0.000 0.000 0.036
#&gt; SRR1927043     3  0.0000      0.990 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927042     1  0.0000      0.987 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      0.987 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927039     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927038     1  0.0000      0.987 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927036     1  0.0963      0.976 0.964 0.000 0.000 0.000 0.036
#&gt; SRR1927035     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927034     4  0.0609      0.968 0.000 0.000 0.000 0.980 0.020
#&gt; SRR1927033     3  0.0794      0.976 0.000 0.000 0.972 0.000 0.028
#&gt; SRR1927032     1  0.0000      0.987 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927031     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927030     1  0.0963      0.976 0.964 0.000 0.000 0.000 0.036
#&gt; SRR1927028     4  0.0000      0.969 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927029     3  0.0000      0.990 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927027     5  0.1671      0.795 0.000 0.000 0.076 0.000 0.924
#&gt; SRR1927026     4  0.0290      0.969 0.000 0.000 0.000 0.992 0.008
#&gt; SRR1927024     4  0.0000      0.969 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927025     5  0.3671      0.682 0.000 0.236 0.008 0.000 0.756
#&gt; SRR1927023     5  0.1549      0.816 0.000 0.016 0.040 0.000 0.944
#&gt; SRR1927022     4  0.3734      0.709 0.168 0.000 0.000 0.796 0.036
#&gt; SRR1927021     2  0.0510      0.982 0.000 0.984 0.000 0.000 0.016
#&gt; SRR1927020     4  0.0609      0.968 0.000 0.000 0.000 0.980 0.020
#&gt; SRR1927019     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927071     4  0.0000      0.969 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927069     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927070     1  0.0963      0.976 0.964 0.000 0.000 0.000 0.036
#&gt; SRR1927068     4  0.0609      0.968 0.000 0.000 0.000 0.980 0.020
#&gt; SRR1927066     4  0.0162      0.968 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1927065     3  0.0000      0.990 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927067     3  0.0000      0.990 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927064     1  0.0000      0.987 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927063     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927062     4  0.0162      0.968 0.000 0.000 0.000 0.996 0.004
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-4-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-5'>
<p><a id='tab-MAD-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1927048     1  0.0458      0.927 0.984 0.000 0.016 0.000 0.000 0.000
#&gt; SRR1927061     3  0.3868      1.000 0.000 0.000 0.508 0.000 0.000 0.492
#&gt; SRR1927060     1  0.0000      0.930 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.0790      0.975 0.000 0.968 0.032 0.000 0.000 0.000
#&gt; SRR1927058     1  0.0000      0.930 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927057     2  0.0790      0.975 0.000 0.968 0.032 0.000 0.000 0.000
#&gt; SRR1927055     6  0.0146      0.476 0.000 0.000 0.000 0.000 0.004 0.996
#&gt; SRR1927056     4  0.0000      0.849 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927054     1  0.0000      0.930 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927052     4  0.3151      0.847 0.000 0.000 0.252 0.748 0.000 0.000
#&gt; SRR1927053     2  0.0790      0.975 0.000 0.968 0.032 0.000 0.000 0.000
#&gt; SRR1927051     2  0.0000      0.977 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927050     4  0.0000      0.849 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927049     2  0.0000      0.977 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927047     2  0.0458      0.977 0.000 0.984 0.016 0.000 0.000 0.000
#&gt; SRR1927046     1  0.2454      0.878 0.840 0.000 0.160 0.000 0.000 0.000
#&gt; SRR1927045     2  0.0508      0.969 0.000 0.984 0.012 0.000 0.004 0.000
#&gt; SRR1927044     1  0.2664      0.867 0.816 0.000 0.184 0.000 0.000 0.000
#&gt; SRR1927043     3  0.3868      1.000 0.000 0.000 0.508 0.000 0.000 0.492
#&gt; SRR1927042     1  0.0000      0.930 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      0.930 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927039     2  0.0790      0.975 0.000 0.968 0.032 0.000 0.000 0.000
#&gt; SRR1927038     1  0.0000      0.930 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.0790      0.975 0.000 0.968 0.032 0.000 0.000 0.000
#&gt; SRR1927036     1  0.2664      0.867 0.816 0.000 0.184 0.000 0.000 0.000
#&gt; SRR1927035     2  0.0000      0.977 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927034     4  0.0000      0.849 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927033     6  0.0405      0.464 0.000 0.000 0.008 0.000 0.004 0.988
#&gt; SRR1927032     1  0.0000      0.930 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927031     2  0.0790      0.975 0.000 0.968 0.032 0.000 0.000 0.000
#&gt; SRR1927030     1  0.2664      0.867 0.816 0.000 0.184 0.000 0.000 0.000
#&gt; SRR1927028     4  0.2697      0.867 0.000 0.000 0.188 0.812 0.000 0.000
#&gt; SRR1927029     3  0.3868      1.000 0.000 0.000 0.508 0.000 0.000 0.492
#&gt; SRR1927027     6  0.4403     -0.168 0.000 0.000 0.024 0.000 0.468 0.508
#&gt; SRR1927026     4  0.1765      0.865 0.000 0.000 0.096 0.904 0.000 0.000
#&gt; SRR1927024     4  0.3076      0.853 0.000 0.000 0.240 0.760 0.000 0.000
#&gt; SRR1927025     5  0.1957      0.760 0.000 0.112 0.000 0.000 0.888 0.000
#&gt; SRR1927023     5  0.0000      0.750 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927022     4  0.5259      0.505 0.096 0.000 0.436 0.468 0.000 0.000
#&gt; SRR1927021     2  0.1663      0.895 0.000 0.912 0.000 0.000 0.088 0.000
#&gt; SRR1927020     4  0.0000      0.849 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927019     2  0.0000      0.977 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927071     4  0.2854      0.864 0.000 0.000 0.208 0.792 0.000 0.000
#&gt; SRR1927069     2  0.0000      0.977 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927070     1  0.2664      0.867 0.816 0.000 0.184 0.000 0.000 0.000
#&gt; SRR1927068     4  0.0000      0.849 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927066     4  0.2969      0.860 0.000 0.000 0.224 0.776 0.000 0.000
#&gt; SRR1927065     3  0.3868      1.000 0.000 0.000 0.508 0.000 0.000 0.492
#&gt; SRR1927067     3  0.3868      1.000 0.000 0.000 0.508 0.000 0.000 0.492
#&gt; SRR1927064     1  0.0146      0.929 0.996 0.000 0.004 0.000 0.000 0.000
#&gt; SRR1927063     2  0.0000      0.977 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927062     4  0.2969      0.860 0.000 0.000 0.224 0.776 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-5-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-signatures'>
<ul>
<li><a href='#tab-MAD-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-skmeans-signature_compare](figure_cola/MAD-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-skmeans-collect-classes](figure_cola/MAD-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:pam*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "pam"]
# you can also extract it by
# res = res_list["MAD:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16868 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 5.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-pam-collect-plots](figure_cola/MAD-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-pam-select-partition-number](figure_cola/MAD-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.999       0.999         0.5095 0.491   0.491
#> 3 3 0.946           0.949       0.975         0.2726 0.841   0.681
#> 4 4 0.910           0.906       0.959         0.1588 0.889   0.687
#> 5 5 0.905           0.837       0.896         0.0519 0.947   0.796
#> 6 6 0.866           0.849       0.881         0.0306 0.977   0.892
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 5
#> attr(,"optional")
#> [1] 2 3 4
```

There is also optional best $k$ = 2 3 4 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-classes'>
<ul>
<li><a href='#tab-MAD-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-pam-get-classes-1'>
<p><a id='tab-MAD-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1927048     1   0.000      1.000 1.000 0.000
#&gt; SRR1927061     2   0.000      0.998 0.000 1.000
#&gt; SRR1927060     1   0.000      1.000 1.000 0.000
#&gt; SRR1927059     2   0.000      0.998 0.000 1.000
#&gt; SRR1927058     1   0.000      1.000 1.000 0.000
#&gt; SRR1927057     2   0.000      0.998 0.000 1.000
#&gt; SRR1927055     2   0.000      0.998 0.000 1.000
#&gt; SRR1927056     1   0.000      1.000 1.000 0.000
#&gt; SRR1927054     1   0.000      1.000 1.000 0.000
#&gt; SRR1927052     1   0.000      1.000 1.000 0.000
#&gt; SRR1927053     2   0.000      0.998 0.000 1.000
#&gt; SRR1927051     2   0.000      0.998 0.000 1.000
#&gt; SRR1927050     1   0.000      1.000 1.000 0.000
#&gt; SRR1927049     2   0.000      0.998 0.000 1.000
#&gt; SRR1927047     2   0.000      0.998 0.000 1.000
#&gt; SRR1927046     1   0.000      1.000 1.000 0.000
#&gt; SRR1927045     2   0.000      0.998 0.000 1.000
#&gt; SRR1927044     1   0.000      1.000 1.000 0.000
#&gt; SRR1927043     2   0.000      0.998 0.000 1.000
#&gt; SRR1927042     1   0.000      1.000 1.000 0.000
#&gt; SRR1927040     1   0.000      1.000 1.000 0.000
#&gt; SRR1927039     2   0.000      0.998 0.000 1.000
#&gt; SRR1927038     1   0.000      1.000 1.000 0.000
#&gt; SRR1927037     2   0.000      0.998 0.000 1.000
#&gt; SRR1927036     1   0.000      1.000 1.000 0.000
#&gt; SRR1927035     2   0.000      0.998 0.000 1.000
#&gt; SRR1927034     1   0.000      1.000 1.000 0.000
#&gt; SRR1927033     2   0.000      0.998 0.000 1.000
#&gt; SRR1927032     1   0.000      1.000 1.000 0.000
#&gt; SRR1927031     2   0.000      0.998 0.000 1.000
#&gt; SRR1927030     1   0.000      1.000 1.000 0.000
#&gt; SRR1927028     1   0.000      1.000 1.000 0.000
#&gt; SRR1927029     2   0.000      0.998 0.000 1.000
#&gt; SRR1927027     2   0.224      0.963 0.036 0.964
#&gt; SRR1927026     1   0.000      1.000 1.000 0.000
#&gt; SRR1927024     1   0.000      1.000 1.000 0.000
#&gt; SRR1927025     2   0.000      0.998 0.000 1.000
#&gt; SRR1927023     2   0.000      0.998 0.000 1.000
#&gt; SRR1927022     1   0.000      1.000 1.000 0.000
#&gt; SRR1927021     2   0.000      0.998 0.000 1.000
#&gt; SRR1927020     1   0.000      1.000 1.000 0.000
#&gt; SRR1927019     2   0.000      0.998 0.000 1.000
#&gt; SRR1927071     1   0.000      1.000 1.000 0.000
#&gt; SRR1927069     2   0.000      0.998 0.000 1.000
#&gt; SRR1927070     1   0.000      1.000 1.000 0.000
#&gt; SRR1927068     1   0.000      1.000 1.000 0.000
#&gt; SRR1927066     1   0.000      1.000 1.000 0.000
#&gt; SRR1927065     2   0.000      0.998 0.000 1.000
#&gt; SRR1927067     2   0.000      0.998 0.000 1.000
#&gt; SRR1927064     1   0.000      1.000 1.000 0.000
#&gt; SRR1927063     2   0.000      0.998 0.000 1.000
#&gt; SRR1927062     1   0.000      1.000 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-1-a').click(function(){
  $('#tab-MAD-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-2'>
<p><a id='tab-MAD-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1927048     1  0.0000      0.942 1.000 0.000 0.000
#&gt; SRR1927061     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927060     1  0.0000      0.942 1.000 0.000 0.000
#&gt; SRR1927059     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927058     1  0.0000      0.942 1.000 0.000 0.000
#&gt; SRR1927057     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927055     2  0.1163      0.970 0.000 0.972 0.028
#&gt; SRR1927056     3  0.0000      0.953 0.000 0.000 1.000
#&gt; SRR1927054     1  0.0000      0.942 1.000 0.000 0.000
#&gt; SRR1927052     1  0.4931      0.774 0.768 0.000 0.232
#&gt; SRR1927053     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927051     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927050     3  0.0000      0.953 0.000 0.000 1.000
#&gt; SRR1927049     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927047     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927046     1  0.0424      0.941 0.992 0.000 0.008
#&gt; SRR1927045     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927044     1  0.3340      0.892 0.880 0.000 0.120
#&gt; SRR1927043     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927042     1  0.0000      0.942 1.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      0.942 1.000 0.000 0.000
#&gt; SRR1927039     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927038     1  0.0000      0.942 1.000 0.000 0.000
#&gt; SRR1927037     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927036     1  0.3340      0.892 0.880 0.000 0.120
#&gt; SRR1927035     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927034     3  0.0000      0.953 0.000 0.000 1.000
#&gt; SRR1927033     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927032     1  0.0000      0.942 1.000 0.000 0.000
#&gt; SRR1927031     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927030     1  0.2066      0.922 0.940 0.000 0.060
#&gt; SRR1927028     3  0.0000      0.953 0.000 0.000 1.000
#&gt; SRR1927029     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927027     3  0.6126      0.323 0.000 0.400 0.600
#&gt; SRR1927026     3  0.0000      0.953 0.000 0.000 1.000
#&gt; SRR1927024     3  0.0000      0.953 0.000 0.000 1.000
#&gt; SRR1927025     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927023     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927022     1  0.4605      0.809 0.796 0.000 0.204
#&gt; SRR1927021     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927020     3  0.0000      0.953 0.000 0.000 1.000
#&gt; SRR1927019     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927071     3  0.0000      0.953 0.000 0.000 1.000
#&gt; SRR1927069     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927070     1  0.3340      0.892 0.880 0.000 0.120
#&gt; SRR1927068     3  0.0000      0.953 0.000 0.000 1.000
#&gt; SRR1927066     3  0.0237      0.949 0.004 0.000 0.996
#&gt; SRR1927065     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927067     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927064     1  0.0000      0.942 1.000 0.000 0.000
#&gt; SRR1927063     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927062     3  0.0000      0.953 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-2-a').click(function(){
  $('#tab-MAD-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-3'>
<p><a id='tab-MAD-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1927048     1  0.0000      0.921 1.000 0.000 0.000 0.000
#&gt; SRR1927061     3  0.0000      0.928 0.000 0.000 1.000 0.000
#&gt; SRR1927060     1  0.0000      0.921 1.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.0000      0.965 0.000 1.000 0.000 0.000
#&gt; SRR1927058     1  0.0000      0.921 1.000 0.000 0.000 0.000
#&gt; SRR1927057     2  0.0000      0.965 0.000 1.000 0.000 0.000
#&gt; SRR1927055     3  0.0000      0.928 0.000 0.000 1.000 0.000
#&gt; SRR1927056     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1927054     1  0.0000      0.921 1.000 0.000 0.000 0.000
#&gt; SRR1927052     1  0.4730      0.536 0.636 0.000 0.000 0.364
#&gt; SRR1927053     2  0.0000      0.965 0.000 1.000 0.000 0.000
#&gt; SRR1927051     2  0.0000      0.965 0.000 1.000 0.000 0.000
#&gt; SRR1927050     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1927049     2  0.0000      0.965 0.000 1.000 0.000 0.000
#&gt; SRR1927047     2  0.0000      0.965 0.000 1.000 0.000 0.000
#&gt; SRR1927046     1  0.0336      0.919 0.992 0.000 0.000 0.008
#&gt; SRR1927045     2  0.1389      0.919 0.000 0.952 0.048 0.000
#&gt; SRR1927044     1  0.2647      0.869 0.880 0.000 0.000 0.120
#&gt; SRR1927043     3  0.0000      0.928 0.000 0.000 1.000 0.000
#&gt; SRR1927042     1  0.0000      0.921 1.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      0.921 1.000 0.000 0.000 0.000
#&gt; SRR1927039     2  0.0000      0.965 0.000 1.000 0.000 0.000
#&gt; SRR1927038     1  0.0000      0.921 1.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.0000      0.965 0.000 1.000 0.000 0.000
#&gt; SRR1927036     1  0.2647      0.869 0.880 0.000 0.000 0.120
#&gt; SRR1927035     2  0.0000      0.965 0.000 1.000 0.000 0.000
#&gt; SRR1927034     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1927033     3  0.0000      0.928 0.000 0.000 1.000 0.000
#&gt; SRR1927032     1  0.0000      0.921 1.000 0.000 0.000 0.000
#&gt; SRR1927031     2  0.0000      0.965 0.000 1.000 0.000 0.000
#&gt; SRR1927030     1  0.1637      0.901 0.940 0.000 0.000 0.060
#&gt; SRR1927028     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1927029     3  0.0000      0.928 0.000 0.000 1.000 0.000
#&gt; SRR1927027     3  0.3610      0.716 0.000 0.000 0.800 0.200
#&gt; SRR1927026     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1927024     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1927025     2  0.4961      0.140 0.000 0.552 0.448 0.000
#&gt; SRR1927023     3  0.4522      0.486 0.000 0.320 0.680 0.000
#&gt; SRR1927022     1  0.4605      0.590 0.664 0.000 0.000 0.336
#&gt; SRR1927021     2  0.0000      0.965 0.000 1.000 0.000 0.000
#&gt; SRR1927020     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1927019     2  0.0000      0.965 0.000 1.000 0.000 0.000
#&gt; SRR1927071     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1927069     2  0.0000      0.965 0.000 1.000 0.000 0.000
#&gt; SRR1927070     1  0.2647      0.869 0.880 0.000 0.000 0.120
#&gt; SRR1927068     4  0.0000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1927066     4  0.0188      0.995 0.004 0.000 0.000 0.996
#&gt; SRR1927065     3  0.0000      0.928 0.000 0.000 1.000 0.000
#&gt; SRR1927067     3  0.0000      0.928 0.000 0.000 1.000 0.000
#&gt; SRR1927064     1  0.0000      0.921 1.000 0.000 0.000 0.000
#&gt; SRR1927063     2  0.0000      0.965 0.000 1.000 0.000 0.000
#&gt; SRR1927062     4  0.0000      1.000 0.000 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-3-a').click(function(){
  $('#tab-MAD-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-4'>
<p><a id='tab-MAD-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1927048     1   0.393      0.825 0.672 0.000 0.000 0.328 0.000
#&gt; SRR1927061     3   0.000      0.892 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927060     1   0.000      0.784 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927059     2   0.000      0.964 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927058     1   0.000      0.784 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927057     2   0.000      0.964 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927055     3   0.000      0.892 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927056     5   0.000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1927054     1   0.000      0.784 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927052     4   0.000      0.674 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927053     2   0.000      0.964 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927051     2   0.000      0.964 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927050     5   0.000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1927049     2   0.000      0.964 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927047     2   0.000      0.964 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927046     1   0.395      0.824 0.668 0.000 0.000 0.332 0.000
#&gt; SRR1927045     2   0.120      0.919 0.000 0.952 0.048 0.000 0.000
#&gt; SRR1927044     1   0.397      0.823 0.664 0.000 0.000 0.336 0.000
#&gt; SRR1927043     3   0.000      0.892 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927042     1   0.395      0.824 0.668 0.000 0.000 0.332 0.000
#&gt; SRR1927040     1   0.000      0.784 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927039     2   0.000      0.964 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927038     1   0.000      0.784 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927037     2   0.000      0.964 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927036     1   0.397      0.823 0.664 0.000 0.000 0.336 0.000
#&gt; SRR1927035     2   0.000      0.964 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927034     5   0.000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1927033     3   0.000      0.892 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927032     1   0.000      0.784 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927031     2   0.000      0.964 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927030     1   0.397      0.823 0.664 0.000 0.000 0.336 0.000
#&gt; SRR1927028     4   0.395      0.718 0.000 0.000 0.000 0.668 0.332
#&gt; SRR1927029     3   0.000      0.892 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927027     3   0.417      0.311 0.000 0.000 0.604 0.000 0.396
#&gt; SRR1927026     4   0.397      0.713 0.000 0.000 0.000 0.664 0.336
#&gt; SRR1927024     4   0.348      0.729 0.000 0.000 0.000 0.752 0.248
#&gt; SRR1927025     2   0.427      0.148 0.000 0.552 0.448 0.000 0.000
#&gt; SRR1927023     3   0.389      0.471 0.000 0.320 0.680 0.000 0.000
#&gt; SRR1927022     4   0.000      0.674 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927021     2   0.000      0.964 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927020     5   0.000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1927019     2   0.000      0.964 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927071     4   0.395      0.718 0.000 0.000 0.000 0.668 0.332
#&gt; SRR1927069     2   0.000      0.964 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927070     1   0.397      0.823 0.664 0.000 0.000 0.336 0.000
#&gt; SRR1927068     5   0.000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1927066     4   0.029      0.678 0.000 0.000 0.000 0.992 0.008
#&gt; SRR1927065     3   0.000      0.892 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927067     3   0.000      0.892 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927064     1   0.377      0.824 0.704 0.000 0.000 0.296 0.000
#&gt; SRR1927063     2   0.000      0.964 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927062     4   0.395      0.718 0.000 0.000 0.000 0.668 0.332
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-4-a').click(function(){
  $('#tab-MAD-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-5'>
<p><a id='tab-MAD-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1927048     1  0.0146      0.825 0.996 0.000 0.000 0.000 0.004 0.000
#&gt; SRR1927061     3  0.0000      0.999 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927060     1  0.3547      0.766 0.668 0.000 0.000 0.000 0.332 0.000
#&gt; SRR1927059     2  0.0000      0.871 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927058     1  0.3547      0.766 0.668 0.000 0.000 0.000 0.332 0.000
#&gt; SRR1927057     2  0.0000      0.871 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927055     3  0.0146      0.997 0.000 0.000 0.996 0.004 0.000 0.000
#&gt; SRR1927056     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1927054     1  0.3547      0.766 0.668 0.000 0.000 0.000 0.332 0.000
#&gt; SRR1927052     4  0.3547      0.661 0.332 0.000 0.000 0.668 0.000 0.000
#&gt; SRR1927053     2  0.0000      0.871 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927051     2  0.2762      0.880 0.000 0.804 0.000 0.196 0.000 0.000
#&gt; SRR1927050     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1927049     2  0.2762      0.880 0.000 0.804 0.000 0.196 0.000 0.000
#&gt; SRR1927047     2  0.0000      0.871 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927046     1  0.0000      0.824 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927045     2  0.4008      0.824 0.000 0.740 0.064 0.196 0.000 0.000
#&gt; SRR1927044     1  0.0146      0.823 0.996 0.000 0.000 0.004 0.000 0.000
#&gt; SRR1927043     3  0.0000      0.999 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927042     1  0.0000      0.824 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.3547      0.766 0.668 0.000 0.000 0.000 0.332 0.000
#&gt; SRR1927039     2  0.0000      0.871 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927038     1  0.3547      0.766 0.668 0.000 0.000 0.000 0.332 0.000
#&gt; SRR1927037     2  0.0000      0.871 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927036     1  0.0146      0.823 0.996 0.000 0.000 0.004 0.000 0.000
#&gt; SRR1927035     2  0.2762      0.880 0.000 0.804 0.000 0.196 0.000 0.000
#&gt; SRR1927034     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1927033     3  0.0146      0.997 0.000 0.000 0.996 0.004 0.000 0.000
#&gt; SRR1927032     1  0.3547      0.766 0.668 0.000 0.000 0.000 0.332 0.000
#&gt; SRR1927031     2  0.0260      0.872 0.000 0.992 0.000 0.008 0.000 0.000
#&gt; SRR1927030     1  0.0146      0.823 0.996 0.000 0.000 0.004 0.000 0.000
#&gt; SRR1927028     4  0.3547      0.714 0.000 0.000 0.000 0.668 0.000 0.332
#&gt; SRR1927029     3  0.0000      0.999 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927027     5  0.5583      0.652 0.000 0.000 0.196 0.136 0.632 0.036
#&gt; SRR1927026     4  0.3563      0.709 0.000 0.000 0.000 0.664 0.000 0.336
#&gt; SRR1927024     4  0.4595      0.726 0.084 0.000 0.000 0.668 0.000 0.248
#&gt; SRR1927025     5  0.3668      0.849 0.000 0.004 0.000 0.328 0.668 0.000
#&gt; SRR1927023     5  0.3668      0.849 0.000 0.004 0.000 0.328 0.668 0.000
#&gt; SRR1927022     4  0.3547      0.661 0.332 0.000 0.000 0.668 0.000 0.000
#&gt; SRR1927021     2  0.2762      0.880 0.000 0.804 0.000 0.196 0.000 0.000
#&gt; SRR1927020     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1927019     2  0.2762      0.880 0.000 0.804 0.000 0.196 0.000 0.000
#&gt; SRR1927071     4  0.3547      0.714 0.000 0.000 0.000 0.668 0.000 0.332
#&gt; SRR1927069     2  0.2762      0.880 0.000 0.804 0.000 0.196 0.000 0.000
#&gt; SRR1927070     1  0.0146      0.823 0.996 0.000 0.000 0.004 0.000 0.000
#&gt; SRR1927068     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1927066     4  0.3758      0.667 0.324 0.000 0.000 0.668 0.000 0.008
#&gt; SRR1927065     3  0.0000      0.999 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927067     3  0.0000      0.999 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927064     1  0.0865      0.824 0.964 0.000 0.000 0.000 0.036 0.000
#&gt; SRR1927063     2  0.2762      0.880 0.000 0.804 0.000 0.196 0.000 0.000
#&gt; SRR1927062     4  0.3547      0.714 0.000 0.000 0.000 0.668 0.000 0.332
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-5-a').click(function(){
  $('#tab-MAD-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-signatures'>
<ul>
<li><a href='#tab-MAD-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-1-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-1"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-2-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-2"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-3-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-3"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-4-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-4"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-5-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-pam-signature_compare](figure_cola/MAD-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-pam-collect-classes](figure_cola/MAD-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:mclust*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "mclust"]
# you can also extract it by
# res = res_list["MAD:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16868 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 5.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-mclust-collect-plots](figure_cola/MAD-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-mclust-select-partition-number](figure_cola/MAD-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5095 0.491   0.491
#> 3 3 0.892           0.956       0.963         0.0955 0.965   0.929
#> 4 4 0.887           0.878       0.929         0.3127 0.813   0.594
#> 5 5 0.929           0.919       0.966         0.0423 0.919   0.726
#> 6 6 0.897           0.915       0.922         0.0488 0.915   0.667
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 5
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-classes'>
<ul>
<li><a href='#tab-MAD-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-mclust-get-classes-1'>
<p><a id='tab-MAD-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1927048     1       0          1  1  0
#&gt; SRR1927061     2       0          1  0  1
#&gt; SRR1927060     1       0          1  1  0
#&gt; SRR1927059     2       0          1  0  1
#&gt; SRR1927058     1       0          1  1  0
#&gt; SRR1927057     2       0          1  0  1
#&gt; SRR1927055     2       0          1  0  1
#&gt; SRR1927056     1       0          1  1  0
#&gt; SRR1927054     1       0          1  1  0
#&gt; SRR1927052     1       0          1  1  0
#&gt; SRR1927053     2       0          1  0  1
#&gt; SRR1927051     2       0          1  0  1
#&gt; SRR1927050     1       0          1  1  0
#&gt; SRR1927049     2       0          1  0  1
#&gt; SRR1927047     2       0          1  0  1
#&gt; SRR1927046     1       0          1  1  0
#&gt; SRR1927045     2       0          1  0  1
#&gt; SRR1927044     1       0          1  1  0
#&gt; SRR1927043     2       0          1  0  1
#&gt; SRR1927042     1       0          1  1  0
#&gt; SRR1927040     1       0          1  1  0
#&gt; SRR1927039     2       0          1  0  1
#&gt; SRR1927038     1       0          1  1  0
#&gt; SRR1927037     2       0          1  0  1
#&gt; SRR1927036     1       0          1  1  0
#&gt; SRR1927035     2       0          1  0  1
#&gt; SRR1927034     1       0          1  1  0
#&gt; SRR1927033     2       0          1  0  1
#&gt; SRR1927032     1       0          1  1  0
#&gt; SRR1927031     2       0          1  0  1
#&gt; SRR1927030     1       0          1  1  0
#&gt; SRR1927028     1       0          1  1  0
#&gt; SRR1927029     2       0          1  0  1
#&gt; SRR1927027     2       0          1  0  1
#&gt; SRR1927026     1       0          1  1  0
#&gt; SRR1927024     1       0          1  1  0
#&gt; SRR1927025     2       0          1  0  1
#&gt; SRR1927023     2       0          1  0  1
#&gt; SRR1927022     1       0          1  1  0
#&gt; SRR1927021     2       0          1  0  1
#&gt; SRR1927020     1       0          1  1  0
#&gt; SRR1927019     2       0          1  0  1
#&gt; SRR1927071     1       0          1  1  0
#&gt; SRR1927069     2       0          1  0  1
#&gt; SRR1927070     1       0          1  1  0
#&gt; SRR1927068     1       0          1  1  0
#&gt; SRR1927066     1       0          1  1  0
#&gt; SRR1927065     2       0          1  0  1
#&gt; SRR1927067     2       0          1  0  1
#&gt; SRR1927064     1       0          1  1  0
#&gt; SRR1927063     2       0          1  0  1
#&gt; SRR1927062     1       0          1  1  0
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-1-a').click(function(){
  $('#tab-MAD-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-2'>
<p><a id='tab-MAD-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1927048     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927061     2  0.3340      0.919 0.000 0.880 0.120
#&gt; SRR1927060     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927059     2  0.0892      0.903 0.000 0.980 0.020
#&gt; SRR1927058     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927057     2  0.1031      0.908 0.000 0.976 0.024
#&gt; SRR1927055     2  0.3941      0.894 0.000 0.844 0.156
#&gt; SRR1927056     1  0.0424      0.996 0.992 0.000 0.008
#&gt; SRR1927054     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927052     1  0.0424      0.996 0.992 0.000 0.008
#&gt; SRR1927053     2  0.0892      0.903 0.000 0.980 0.020
#&gt; SRR1927051     2  0.3192      0.920 0.000 0.888 0.112
#&gt; SRR1927050     1  0.0424      0.996 0.992 0.000 0.008
#&gt; SRR1927049     2  0.3267      0.920 0.000 0.884 0.116
#&gt; SRR1927047     2  0.0892      0.903 0.000 0.980 0.020
#&gt; SRR1927046     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927045     2  0.3192      0.920 0.000 0.888 0.112
#&gt; SRR1927044     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927043     2  0.3340      0.919 0.000 0.880 0.120
#&gt; SRR1927042     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927039     2  0.0892      0.903 0.000 0.980 0.020
#&gt; SRR1927038     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927037     2  0.0892      0.903 0.000 0.980 0.020
#&gt; SRR1927036     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927035     2  0.0892      0.903 0.000 0.980 0.020
#&gt; SRR1927034     1  0.0424      0.996 0.992 0.000 0.008
#&gt; SRR1927033     2  0.5016      0.804 0.000 0.760 0.240
#&gt; SRR1927032     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927031     2  0.0892      0.903 0.000 0.980 0.020
#&gt; SRR1927030     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927028     1  0.0424      0.996 0.992 0.000 0.008
#&gt; SRR1927029     2  0.3340      0.919 0.000 0.880 0.120
#&gt; SRR1927027     3  0.1163      0.991 0.000 0.028 0.972
#&gt; SRR1927026     1  0.0424      0.996 0.992 0.000 0.008
#&gt; SRR1927024     1  0.0424      0.996 0.992 0.000 0.008
#&gt; SRR1927025     2  0.3192      0.917 0.000 0.888 0.112
#&gt; SRR1927023     3  0.1411      0.991 0.000 0.036 0.964
#&gt; SRR1927022     1  0.0424      0.996 0.992 0.000 0.008
#&gt; SRR1927021     2  0.0592      0.906 0.000 0.988 0.012
#&gt; SRR1927020     1  0.0424      0.996 0.992 0.000 0.008
#&gt; SRR1927019     2  0.3267      0.920 0.000 0.884 0.116
#&gt; SRR1927071     1  0.0424      0.996 0.992 0.000 0.008
#&gt; SRR1927069     2  0.0892      0.903 0.000 0.980 0.020
#&gt; SRR1927070     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927068     1  0.0424      0.996 0.992 0.000 0.008
#&gt; SRR1927066     1  0.0424      0.996 0.992 0.000 0.008
#&gt; SRR1927065     2  0.3340      0.919 0.000 0.880 0.120
#&gt; SRR1927067     2  0.3340      0.919 0.000 0.880 0.120
#&gt; SRR1927064     1  0.0000      0.996 1.000 0.000 0.000
#&gt; SRR1927063     2  0.3340      0.919 0.000 0.880 0.120
#&gt; SRR1927062     1  0.0424      0.996 0.992 0.000 0.008
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-2-a').click(function(){
  $('#tab-MAD-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-3'>
<p><a id='tab-MAD-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1927048     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927061     2  0.4585      0.626 0.000 0.668 0.332 0.000
#&gt; SRR1927060     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.0000      0.847 0.000 1.000 0.000 0.000
#&gt; SRR1927058     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927057     2  0.1716      0.830 0.000 0.936 0.064 0.000
#&gt; SRR1927055     3  0.0000      0.911 0.000 0.000 1.000 0.000
#&gt; SRR1927056     4  0.0817      0.961 0.024 0.000 0.000 0.976
#&gt; SRR1927054     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927052     4  0.2868      0.881 0.136 0.000 0.000 0.864
#&gt; SRR1927053     2  0.0000      0.847 0.000 1.000 0.000 0.000
#&gt; SRR1927051     2  0.2334      0.842 0.000 0.908 0.088 0.004
#&gt; SRR1927050     4  0.0817      0.961 0.024 0.000 0.000 0.976
#&gt; SRR1927049     2  0.2334      0.842 0.000 0.908 0.088 0.004
#&gt; SRR1927047     2  0.0000      0.847 0.000 1.000 0.000 0.000
#&gt; SRR1927046     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927045     2  0.2149      0.843 0.000 0.912 0.088 0.000
#&gt; SRR1927044     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927043     2  0.4967      0.440 0.000 0.548 0.452 0.000
#&gt; SRR1927042     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927039     2  0.0000      0.847 0.000 1.000 0.000 0.000
#&gt; SRR1927038     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.0000      0.847 0.000 1.000 0.000 0.000
#&gt; SRR1927036     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927035     2  0.0000      0.847 0.000 1.000 0.000 0.000
#&gt; SRR1927034     4  0.0817      0.961 0.024 0.000 0.000 0.976
#&gt; SRR1927033     3  0.0000      0.911 0.000 0.000 1.000 0.000
#&gt; SRR1927032     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927031     2  0.0000      0.847 0.000 1.000 0.000 0.000
#&gt; SRR1927030     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927028     4  0.0921      0.961 0.028 0.000 0.000 0.972
#&gt; SRR1927029     2  0.4981      0.415 0.000 0.536 0.464 0.000
#&gt; SRR1927027     3  0.0817      0.907 0.000 0.000 0.976 0.024
#&gt; SRR1927026     4  0.0921      0.961 0.028 0.000 0.000 0.972
#&gt; SRR1927024     4  0.1637      0.943 0.060 0.000 0.000 0.940
#&gt; SRR1927025     3  0.3908      0.718 0.000 0.212 0.784 0.004
#&gt; SRR1927023     3  0.2443      0.887 0.000 0.060 0.916 0.024
#&gt; SRR1927022     4  0.3400      0.830 0.180 0.000 0.000 0.820
#&gt; SRR1927021     2  0.1978      0.844 0.000 0.928 0.068 0.004
#&gt; SRR1927020     4  0.0817      0.961 0.024 0.000 0.000 0.976
#&gt; SRR1927019     2  0.2334      0.842 0.000 0.908 0.088 0.004
#&gt; SRR1927071     4  0.0921      0.961 0.028 0.000 0.000 0.972
#&gt; SRR1927069     2  0.0000      0.847 0.000 1.000 0.000 0.000
#&gt; SRR1927070     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927068     4  0.0817      0.961 0.024 0.000 0.000 0.976
#&gt; SRR1927066     4  0.0921      0.961 0.028 0.000 0.000 0.972
#&gt; SRR1927065     2  0.4730      0.584 0.000 0.636 0.364 0.000
#&gt; SRR1927067     2  0.4981      0.415 0.000 0.536 0.464 0.000
#&gt; SRR1927064     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR1927063     2  0.2401      0.841 0.000 0.904 0.092 0.004
#&gt; SRR1927062     4  0.2345      0.913 0.100 0.000 0.000 0.900
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-3-a').click(function(){
  $('#tab-MAD-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-4'>
<p><a id='tab-MAD-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1927048     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927061     3  0.3876      0.528 0.000 0.316 0.684 0.000 0.000
#&gt; SRR1927060     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.0000      0.964 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927058     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927057     2  0.0000      0.964 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927055     3  0.0000      0.834 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927056     4  0.0000      0.930 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927054     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927052     4  0.3039      0.756 0.192 0.000 0.000 0.808 0.000
#&gt; SRR1927053     2  0.0000      0.964 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927051     2  0.0000      0.964 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927050     4  0.0000      0.930 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927049     2  0.1908      0.905 0.000 0.908 0.000 0.000 0.092
#&gt; SRR1927047     2  0.0000      0.964 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927046     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927045     2  0.1671      0.918 0.000 0.924 0.000 0.000 0.076
#&gt; SRR1927044     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927043     3  0.0162      0.833 0.000 0.004 0.996 0.000 0.000
#&gt; SRR1927042     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927039     2  0.0000      0.964 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927038     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.0000      0.964 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927036     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927035     2  0.0000      0.964 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927034     4  0.0000      0.930 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927033     3  0.0404      0.828 0.000 0.000 0.988 0.000 0.012
#&gt; SRR1927032     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927031     2  0.0000      0.964 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927030     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927028     4  0.0000      0.930 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927029     3  0.0000      0.834 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927027     5  0.0609      0.981 0.000 0.000 0.020 0.000 0.980
#&gt; SRR1927026     4  0.0000      0.930 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927024     4  0.0000      0.930 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927025     2  0.3607      0.722 0.000 0.752 0.004 0.000 0.244
#&gt; SRR1927023     5  0.0000      0.981 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1927022     4  0.3242      0.726 0.216 0.000 0.000 0.784 0.000
#&gt; SRR1927021     2  0.0162      0.962 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1927020     4  0.0000      0.930 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927019     2  0.0000      0.964 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927071     4  0.0000      0.930 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927069     2  0.0000      0.964 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927070     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927068     4  0.0000      0.930 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927066     4  0.0000      0.930 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927065     3  0.4167      0.594 0.000 0.252 0.724 0.000 0.024
#&gt; SRR1927067     3  0.0000      0.834 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927064     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927063     2  0.2824      0.874 0.000 0.872 0.032 0.000 0.096
#&gt; SRR1927062     4  0.3109      0.747 0.200 0.000 0.000 0.800 0.000
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-4-a').click(function(){
  $('#tab-MAD-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-5'>
<p><a id='tab-MAD-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1927048     1  0.0000      0.982 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927061     6  0.3806      0.815 0.000 0.164 0.068 0.000 0.000 0.768
#&gt; SRR1927060     1  0.0260      0.981 0.992 0.000 0.000 0.000 0.000 0.008
#&gt; SRR1927059     2  0.0000      0.975 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927058     1  0.0000      0.982 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927057     6  0.3076      0.870 0.000 0.240 0.000 0.000 0.000 0.760
#&gt; SRR1927055     3  0.0806      0.974 0.000 0.000 0.972 0.000 0.008 0.020
#&gt; SRR1927056     4  0.0260      0.927 0.000 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1927054     1  0.0260      0.981 0.992 0.000 0.000 0.000 0.000 0.008
#&gt; SRR1927052     4  0.1196      0.897 0.040 0.000 0.000 0.952 0.000 0.008
#&gt; SRR1927053     2  0.0146      0.974 0.000 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1927051     6  0.3445      0.868 0.000 0.260 0.008 0.000 0.000 0.732
#&gt; SRR1927050     4  0.2562      0.843 0.000 0.000 0.000 0.828 0.000 0.172
#&gt; SRR1927049     6  0.3494      0.871 0.000 0.252 0.012 0.000 0.000 0.736
#&gt; SRR1927047     2  0.0000      0.975 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927046     1  0.0000      0.982 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927045     6  0.3795      0.771 0.000 0.364 0.004 0.000 0.000 0.632
#&gt; SRR1927044     1  0.0000      0.982 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927043     3  0.0520      0.970 0.000 0.008 0.984 0.000 0.000 0.008
#&gt; SRR1927042     1  0.0000      0.982 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0260      0.981 0.992 0.000 0.000 0.000 0.000 0.008
#&gt; SRR1927039     2  0.0146      0.974 0.000 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1927038     1  0.0260      0.981 0.992 0.000 0.000 0.000 0.000 0.008
#&gt; SRR1927037     6  0.3737      0.734 0.000 0.392 0.000 0.000 0.000 0.608
#&gt; SRR1927036     1  0.0146      0.980 0.996 0.000 0.000 0.004 0.000 0.000
#&gt; SRR1927035     2  0.0363      0.963 0.000 0.988 0.000 0.000 0.000 0.012
#&gt; SRR1927034     4  0.2562      0.843 0.000 0.000 0.000 0.828 0.000 0.172
#&gt; SRR1927033     3  0.1003      0.970 0.000 0.000 0.964 0.000 0.016 0.020
#&gt; SRR1927032     1  0.0363      0.979 0.988 0.000 0.000 0.000 0.000 0.012
#&gt; SRR1927031     2  0.0000      0.975 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927030     1  0.0000      0.982 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927028     4  0.0000      0.927 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927029     3  0.0000      0.979 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927027     5  0.1950      0.911 0.000 0.000 0.064 0.000 0.912 0.024
#&gt; SRR1927026     4  0.0000      0.927 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927024     4  0.2664      0.833 0.000 0.000 0.000 0.816 0.000 0.184
#&gt; SRR1927025     2  0.1644      0.903 0.000 0.920 0.000 0.000 0.076 0.004
#&gt; SRR1927023     5  0.0000      0.916 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927022     1  0.2778      0.768 0.824 0.000 0.000 0.168 0.000 0.008
#&gt; SRR1927021     2  0.1075      0.934 0.000 0.952 0.000 0.000 0.048 0.000
#&gt; SRR1927020     4  0.0260      0.927 0.000 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1927019     6  0.3394      0.873 0.000 0.236 0.012 0.000 0.000 0.752
#&gt; SRR1927071     4  0.0146      0.926 0.000 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1927069     2  0.0000      0.975 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927070     1  0.0000      0.982 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927068     4  0.0260      0.927 0.000 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1927066     4  0.0000      0.927 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927065     6  0.5662      0.386 0.000 0.156 0.384 0.000 0.000 0.460
#&gt; SRR1927067     3  0.0000      0.979 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927064     1  0.0363      0.979 0.988 0.000 0.000 0.000 0.000 0.012
#&gt; SRR1927063     6  0.3342      0.870 0.000 0.228 0.012 0.000 0.000 0.760
#&gt; SRR1927062     4  0.2300      0.770 0.144 0.000 0.000 0.856 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-5-a').click(function(){
  $('#tab-MAD-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-signatures'>
<ul>
<li><a href='#tab-MAD-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-1-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-1"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-2-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-2"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-3-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-3"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-4-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-4"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-5-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-mclust-signature_compare](figure_cola/MAD-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-mclust-collect-classes](figure_cola/MAD-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:NMF**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "NMF"]
# you can also extract it by
# res = res_list["MAD:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16868 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-NMF-collect-plots](figure_cola/MAD-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-NMF-select-partition-number](figure_cola/MAD-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5095 0.491   0.491
#> 3 3 0.853           0.829       0.919         0.1490 0.906   0.811
#> 4 4 0.649           0.653       0.792         0.1161 0.910   0.804
#> 5 5 0.694           0.779       0.811         0.1239 0.759   0.460
#> 6 6 0.655           0.734       0.812         0.0264 0.972   0.883
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-classes'>
<ul>
<li><a href='#tab-MAD-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-NMF-get-classes-1'>
<p><a id='tab-MAD-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1927048     1       0          1  1  0
#&gt; SRR1927061     2       0          1  0  1
#&gt; SRR1927060     1       0          1  1  0
#&gt; SRR1927059     2       0          1  0  1
#&gt; SRR1927058     1       0          1  1  0
#&gt; SRR1927057     2       0          1  0  1
#&gt; SRR1927055     2       0          1  0  1
#&gt; SRR1927056     1       0          1  1  0
#&gt; SRR1927054     1       0          1  1  0
#&gt; SRR1927052     1       0          1  1  0
#&gt; SRR1927053     2       0          1  0  1
#&gt; SRR1927051     2       0          1  0  1
#&gt; SRR1927050     1       0          1  1  0
#&gt; SRR1927049     2       0          1  0  1
#&gt; SRR1927047     2       0          1  0  1
#&gt; SRR1927046     1       0          1  1  0
#&gt; SRR1927045     2       0          1  0  1
#&gt; SRR1927044     1       0          1  1  0
#&gt; SRR1927043     2       0          1  0  1
#&gt; SRR1927042     1       0          1  1  0
#&gt; SRR1927040     1       0          1  1  0
#&gt; SRR1927039     2       0          1  0  1
#&gt; SRR1927038     1       0          1  1  0
#&gt; SRR1927037     2       0          1  0  1
#&gt; SRR1927036     1       0          1  1  0
#&gt; SRR1927035     2       0          1  0  1
#&gt; SRR1927034     1       0          1  1  0
#&gt; SRR1927033     2       0          1  0  1
#&gt; SRR1927032     1       0          1  1  0
#&gt; SRR1927031     2       0          1  0  1
#&gt; SRR1927030     1       0          1  1  0
#&gt; SRR1927028     1       0          1  1  0
#&gt; SRR1927029     2       0          1  0  1
#&gt; SRR1927027     2       0          1  0  1
#&gt; SRR1927026     1       0          1  1  0
#&gt; SRR1927024     1       0          1  1  0
#&gt; SRR1927025     2       0          1  0  1
#&gt; SRR1927023     2       0          1  0  1
#&gt; SRR1927022     1       0          1  1  0
#&gt; SRR1927021     2       0          1  0  1
#&gt; SRR1927020     1       0          1  1  0
#&gt; SRR1927019     2       0          1  0  1
#&gt; SRR1927071     1       0          1  1  0
#&gt; SRR1927069     2       0          1  0  1
#&gt; SRR1927070     1       0          1  1  0
#&gt; SRR1927068     1       0          1  1  0
#&gt; SRR1927066     1       0          1  1  0
#&gt; SRR1927065     2       0          1  0  1
#&gt; SRR1927067     2       0          1  0  1
#&gt; SRR1927064     1       0          1  1  0
#&gt; SRR1927063     2       0          1  0  1
#&gt; SRR1927062     1       0          1  1  0
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-1-a').click(function(){
  $('#tab-MAD-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-2'>
<p><a id='tab-MAD-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1927048     1  0.5760      0.402 0.672 0.000 0.328
#&gt; SRR1927061     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927060     3  0.6299      0.264 0.476 0.000 0.524
#&gt; SRR1927059     2  0.6225      0.238 0.000 0.568 0.432
#&gt; SRR1927058     1  0.2625      0.863 0.916 0.000 0.084
#&gt; SRR1927057     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927055     2  0.0237      0.975 0.000 0.996 0.004
#&gt; SRR1927056     1  0.0000      0.899 1.000 0.000 0.000
#&gt; SRR1927054     1  0.5968      0.277 0.636 0.000 0.364
#&gt; SRR1927052     1  0.0000      0.899 1.000 0.000 0.000
#&gt; SRR1927053     3  0.5363      0.352 0.000 0.276 0.724
#&gt; SRR1927051     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927050     1  0.0237      0.896 0.996 0.000 0.004
#&gt; SRR1927049     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927047     2  0.0424      0.970 0.000 0.992 0.008
#&gt; SRR1927046     1  0.2066      0.881 0.940 0.000 0.060
#&gt; SRR1927045     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927044     1  0.2066      0.881 0.940 0.000 0.060
#&gt; SRR1927043     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927042     1  0.3752      0.795 0.856 0.000 0.144
#&gt; SRR1927040     3  0.6299      0.264 0.476 0.000 0.524
#&gt; SRR1927039     3  0.4931      0.411 0.000 0.232 0.768
#&gt; SRR1927038     3  0.6154      0.376 0.408 0.000 0.592
#&gt; SRR1927037     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927036     1  0.1964      0.883 0.944 0.000 0.056
#&gt; SRR1927035     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927034     1  0.0592      0.890 0.988 0.000 0.012
#&gt; SRR1927033     2  0.0747      0.964 0.000 0.984 0.016
#&gt; SRR1927032     1  0.5178      0.598 0.744 0.000 0.256
#&gt; SRR1927031     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927030     1  0.2066      0.881 0.940 0.000 0.060
#&gt; SRR1927028     1  0.0000      0.899 1.000 0.000 0.000
#&gt; SRR1927029     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927027     2  0.0237      0.975 0.000 0.996 0.004
#&gt; SRR1927026     1  0.0000      0.899 1.000 0.000 0.000
#&gt; SRR1927024     1  0.0000      0.899 1.000 0.000 0.000
#&gt; SRR1927025     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927023     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927022     1  0.0592      0.897 0.988 0.000 0.012
#&gt; SRR1927021     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927020     1  0.0000      0.899 1.000 0.000 0.000
#&gt; SRR1927019     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927071     1  0.0000      0.899 1.000 0.000 0.000
#&gt; SRR1927069     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927070     1  0.1964      0.883 0.944 0.000 0.056
#&gt; SRR1927068     1  0.0000      0.899 1.000 0.000 0.000
#&gt; SRR1927066     1  0.0000      0.899 1.000 0.000 0.000
#&gt; SRR1927065     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927067     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927064     1  0.4452      0.724 0.808 0.000 0.192
#&gt; SRR1927063     2  0.0000      0.978 0.000 1.000 0.000
#&gt; SRR1927062     1  0.0000      0.899 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-2-a').click(function(){
  $('#tab-MAD-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-3'>
<p><a id='tab-MAD-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1927048     1  0.3569      0.640 0.804 0.000 0.000 0.196
#&gt; SRR1927061     2  0.0000      0.669 0.000 1.000 0.000 0.000
#&gt; SRR1927060     1  0.4250      0.548 0.724 0.000 0.000 0.276
#&gt; SRR1927059     2  0.4382      0.506 0.000 0.704 0.000 0.296
#&gt; SRR1927058     1  0.0000      0.768 1.000 0.000 0.000 0.000
#&gt; SRR1927057     2  0.2760      0.695 0.000 0.872 0.000 0.128
#&gt; SRR1927055     2  0.1940      0.638 0.000 0.924 0.000 0.076
#&gt; SRR1927056     1  0.4585      0.765 0.668 0.000 0.332 0.000
#&gt; SRR1927054     1  0.3444      0.649 0.816 0.000 0.000 0.184
#&gt; SRR1927052     1  0.4585      0.765 0.668 0.000 0.332 0.000
#&gt; SRR1927053     4  0.4697      0.791 0.000 0.356 0.000 0.644
#&gt; SRR1927051     2  0.3400      0.685 0.000 0.820 0.000 0.180
#&gt; SRR1927050     1  0.4585      0.765 0.668 0.000 0.332 0.000
#&gt; SRR1927049     2  0.3266      0.690 0.000 0.832 0.000 0.168
#&gt; SRR1927047     2  0.4193      0.569 0.000 0.732 0.000 0.268
#&gt; SRR1927046     1  0.0336      0.770 0.992 0.000 0.008 0.000
#&gt; SRR1927045     2  0.1637      0.650 0.000 0.940 0.000 0.060
#&gt; SRR1927044     1  0.0000      0.768 1.000 0.000 0.000 0.000
#&gt; SRR1927043     2  0.1940      0.638 0.000 0.924 0.000 0.076
#&gt; SRR1927042     1  0.1118      0.754 0.964 0.000 0.000 0.036
#&gt; SRR1927040     1  0.4222      0.554 0.728 0.000 0.000 0.272
#&gt; SRR1927039     4  0.4250      0.783 0.000 0.276 0.000 0.724
#&gt; SRR1927038     1  0.4543      0.482 0.676 0.000 0.000 0.324
#&gt; SRR1927037     2  0.3649      0.664 0.000 0.796 0.000 0.204
#&gt; SRR1927036     1  0.1389      0.775 0.952 0.000 0.048 0.000
#&gt; SRR1927035     2  0.3356      0.687 0.000 0.824 0.000 0.176
#&gt; SRR1927034     1  0.4643      0.759 0.656 0.000 0.344 0.000
#&gt; SRR1927033     2  0.4163      0.490 0.000 0.828 0.096 0.076
#&gt; SRR1927032     1  0.1716      0.739 0.936 0.000 0.000 0.064
#&gt; SRR1927031     2  0.3801      0.646 0.000 0.780 0.000 0.220
#&gt; SRR1927030     1  0.0000      0.768 1.000 0.000 0.000 0.000
#&gt; SRR1927028     1  0.4585      0.765 0.668 0.000 0.332 0.000
#&gt; SRR1927029     2  0.1940      0.638 0.000 0.924 0.000 0.076
#&gt; SRR1927027     3  0.6443      0.495 0.000 0.376 0.548 0.076
#&gt; SRR1927026     1  0.4585      0.765 0.668 0.000 0.332 0.000
#&gt; SRR1927024     1  0.4866      0.721 0.596 0.000 0.404 0.000
#&gt; SRR1927025     2  0.7603     -0.215 0.000 0.436 0.360 0.204
#&gt; SRR1927023     3  0.7318      0.299 0.000 0.196 0.524 0.280
#&gt; SRR1927022     1  0.4193      0.774 0.732 0.000 0.268 0.000
#&gt; SRR1927021     2  0.7512     -0.069 0.000 0.496 0.268 0.236
#&gt; SRR1927020     1  0.4624      0.761 0.660 0.000 0.340 0.000
#&gt; SRR1927019     2  0.3400      0.685 0.000 0.820 0.000 0.180
#&gt; SRR1927071     1  0.4585      0.765 0.668 0.000 0.332 0.000
#&gt; SRR1927069     2  0.3764      0.651 0.000 0.784 0.000 0.216
#&gt; SRR1927070     1  0.0000      0.768 1.000 0.000 0.000 0.000
#&gt; SRR1927068     1  0.4564      0.767 0.672 0.000 0.328 0.000
#&gt; SRR1927066     1  0.4564      0.767 0.672 0.000 0.328 0.000
#&gt; SRR1927065     2  0.1557      0.652 0.000 0.944 0.000 0.056
#&gt; SRR1927067     2  0.1637      0.650 0.000 0.940 0.000 0.060
#&gt; SRR1927064     1  0.1211      0.752 0.960 0.000 0.000 0.040
#&gt; SRR1927063     2  0.3024      0.694 0.000 0.852 0.000 0.148
#&gt; SRR1927062     1  0.3837      0.777 0.776 0.000 0.224 0.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-3-a').click(function(){
  $('#tab-MAD-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-4'>
<p><a id='tab-MAD-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1927048     1  0.1478      0.869 0.936 0.000 0.064 0.000 0.000
#&gt; SRR1927061     2  0.4449     -0.662 0.000 0.512 0.484 0.000 0.004
#&gt; SRR1927060     1  0.0794      0.902 0.972 0.000 0.028 0.000 0.000
#&gt; SRR1927059     2  0.1844      0.752 0.012 0.936 0.040 0.000 0.012
#&gt; SRR1927058     1  0.1197      0.910 0.952 0.000 0.000 0.048 0.000
#&gt; SRR1927057     2  0.2707      0.632 0.000 0.860 0.132 0.000 0.008
#&gt; SRR1927055     3  0.4873      0.904 0.000 0.312 0.644 0.000 0.044
#&gt; SRR1927056     4  0.3534      0.938 0.256 0.000 0.000 0.744 0.000
#&gt; SRR1927054     1  0.0162      0.914 0.996 0.000 0.004 0.000 0.000
#&gt; SRR1927052     4  0.3586      0.937 0.264 0.000 0.000 0.736 0.000
#&gt; SRR1927053     2  0.5191      0.498 0.048 0.688 0.244 0.004 0.016
#&gt; SRR1927051     2  0.0794      0.757 0.000 0.972 0.028 0.000 0.000
#&gt; SRR1927050     4  0.3715      0.938 0.260 0.000 0.004 0.736 0.000
#&gt; SRR1927049     2  0.1197      0.747 0.000 0.952 0.048 0.000 0.000
#&gt; SRR1927047     2  0.2069      0.745 0.012 0.924 0.052 0.000 0.012
#&gt; SRR1927046     1  0.0794      0.917 0.972 0.000 0.000 0.028 0.000
#&gt; SRR1927045     3  0.4517      0.897 0.000 0.388 0.600 0.000 0.012
#&gt; SRR1927044     1  0.1270      0.908 0.948 0.000 0.000 0.052 0.000
#&gt; SRR1927043     3  0.4030      0.925 0.000 0.352 0.648 0.000 0.000
#&gt; SRR1927042     1  0.0290      0.917 0.992 0.000 0.000 0.008 0.000
#&gt; SRR1927040     1  0.0880      0.899 0.968 0.000 0.032 0.000 0.000
#&gt; SRR1927039     2  0.4669      0.594 0.044 0.752 0.184 0.004 0.016
#&gt; SRR1927038     1  0.1270      0.882 0.948 0.000 0.052 0.000 0.000
#&gt; SRR1927037     2  0.1106      0.758 0.000 0.964 0.024 0.000 0.012
#&gt; SRR1927036     1  0.1544      0.893 0.932 0.000 0.000 0.068 0.000
#&gt; SRR1927035     2  0.0880      0.757 0.000 0.968 0.032 0.000 0.000
#&gt; SRR1927034     4  0.2609      0.665 0.068 0.000 0.028 0.896 0.008
#&gt; SRR1927033     3  0.5470      0.852 0.000 0.296 0.612 0.000 0.092
#&gt; SRR1927032     1  0.0703      0.917 0.976 0.000 0.000 0.024 0.000
#&gt; SRR1927031     2  0.0404      0.761 0.000 0.988 0.000 0.000 0.012
#&gt; SRR1927030     1  0.1270      0.908 0.948 0.000 0.000 0.052 0.000
#&gt; SRR1927028     4  0.3561      0.939 0.260 0.000 0.000 0.740 0.000
#&gt; SRR1927029     3  0.4101      0.919 0.000 0.332 0.664 0.004 0.000
#&gt; SRR1927027     5  0.3687      0.707 0.000 0.028 0.180 0.000 0.792
#&gt; SRR1927026     4  0.3586      0.937 0.264 0.000 0.000 0.736 0.000
#&gt; SRR1927024     4  0.5917      0.784 0.224 0.000 0.000 0.596 0.180
#&gt; SRR1927025     5  0.4756      0.588 0.000 0.288 0.044 0.000 0.668
#&gt; SRR1927023     5  0.1800      0.760 0.000 0.048 0.020 0.000 0.932
#&gt; SRR1927022     1  0.4060      0.138 0.640 0.000 0.000 0.360 0.000
#&gt; SRR1927021     2  0.4969      0.144 0.000 0.588 0.036 0.000 0.376
#&gt; SRR1927020     4  0.3452      0.930 0.244 0.000 0.000 0.756 0.000
#&gt; SRR1927019     2  0.1408      0.748 0.000 0.948 0.044 0.000 0.008
#&gt; SRR1927071     4  0.3561      0.939 0.260 0.000 0.000 0.740 0.000
#&gt; SRR1927069     2  0.3035      0.696 0.000 0.856 0.032 0.000 0.112
#&gt; SRR1927070     1  0.1270      0.908 0.948 0.000 0.000 0.052 0.000
#&gt; SRR1927068     4  0.3534      0.938 0.256 0.000 0.000 0.744 0.000
#&gt; SRR1927066     4  0.3586      0.937 0.264 0.000 0.000 0.736 0.000
#&gt; SRR1927065     3  0.4101      0.917 0.000 0.372 0.628 0.000 0.000
#&gt; SRR1927067     3  0.4150      0.886 0.000 0.388 0.612 0.000 0.000
#&gt; SRR1927064     1  0.0807      0.916 0.976 0.000 0.012 0.012 0.000
#&gt; SRR1927063     2  0.2304      0.685 0.000 0.892 0.100 0.000 0.008
#&gt; SRR1927062     4  0.4084      0.856 0.328 0.000 0.004 0.668 0.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-4-a').click(function(){
  $('#tab-MAD-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-5'>
<p><a id='tab-MAD-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5 p6
#&gt; SRR1927048     1  0.1882      0.852 0.920 0.000 0.008 0.012 0.000 NA
#&gt; SRR1927061     2  0.3765     -0.249 0.000 0.596 0.404 0.000 0.000 NA
#&gt; SRR1927060     1  0.0260      0.901 0.992 0.000 0.000 0.000 0.000 NA
#&gt; SRR1927059     2  0.2485      0.707 0.024 0.884 0.000 0.000 0.008 NA
#&gt; SRR1927058     1  0.1610      0.910 0.916 0.000 0.000 0.084 0.000 NA
#&gt; SRR1927057     2  0.2673      0.619 0.000 0.852 0.132 0.000 0.004 NA
#&gt; SRR1927055     3  0.4029      0.852 0.000 0.292 0.680 0.000 0.028 NA
#&gt; SRR1927056     4  0.2595      0.899 0.160 0.000 0.000 0.836 0.000 NA
#&gt; SRR1927054     1  0.0632      0.914 0.976 0.000 0.000 0.024 0.000 NA
#&gt; SRR1927052     4  0.2946      0.898 0.176 0.000 0.000 0.812 0.000 NA
#&gt; SRR1927053     2  0.4949      0.427 0.072 0.636 0.000 0.000 0.012 NA
#&gt; SRR1927051     2  0.1261      0.726 0.000 0.952 0.024 0.000 0.000 NA
#&gt; SRR1927050     4  0.3246      0.893 0.160 0.000 0.012 0.812 0.000 NA
#&gt; SRR1927049     2  0.1219      0.715 0.000 0.948 0.048 0.000 0.000 NA
#&gt; SRR1927047     2  0.2350      0.719 0.008 0.900 0.004 0.000 0.024 NA
#&gt; SRR1927046     1  0.1806      0.908 0.908 0.000 0.000 0.088 0.000 NA
#&gt; SRR1927045     3  0.3867      0.854 0.000 0.328 0.660 0.000 0.012 NA
#&gt; SRR1927044     1  0.1610      0.910 0.916 0.000 0.000 0.084 0.000 NA
#&gt; SRR1927043     3  0.3620      0.832 0.000 0.352 0.648 0.000 0.000 NA
#&gt; SRR1927042     1  0.0790      0.915 0.968 0.000 0.000 0.032 0.000 NA
#&gt; SRR1927040     1  0.0520      0.905 0.984 0.000 0.000 0.008 0.000 NA
#&gt; SRR1927039     2  0.5144      0.475 0.068 0.668 0.004 0.000 0.032 NA
#&gt; SRR1927038     1  0.0713      0.885 0.972 0.000 0.000 0.000 0.000 NA
#&gt; SRR1927037     2  0.0692      0.731 0.000 0.976 0.000 0.000 0.004 NA
#&gt; SRR1927036     1  0.1910      0.897 0.892 0.000 0.000 0.108 0.000 NA
#&gt; SRR1927035     2  0.2563      0.701 0.000 0.880 0.040 0.000 0.004 NA
#&gt; SRR1927034     4  0.3127      0.688 0.044 0.000 0.020 0.852 0.000 NA
#&gt; SRR1927033     3  0.4844      0.812 0.000 0.272 0.652 0.000 0.060 NA
#&gt; SRR1927032     1  0.1285      0.916 0.944 0.000 0.000 0.052 0.000 NA
#&gt; SRR1927031     2  0.1989      0.724 0.000 0.916 0.004 0.000 0.052 NA
#&gt; SRR1927030     1  0.1663      0.908 0.912 0.000 0.000 0.088 0.000 NA
#&gt; SRR1927028     4  0.2909      0.897 0.156 0.000 0.004 0.828 0.000 NA
#&gt; SRR1927029     3  0.3547      0.849 0.000 0.300 0.696 0.000 0.000 NA
#&gt; SRR1927027     5  0.5398      0.523 0.000 0.056 0.216 0.000 0.652 NA
#&gt; SRR1927026     4  0.3404      0.886 0.184 0.000 0.004 0.792 0.012 NA
#&gt; SRR1927024     4  0.6064      0.545 0.152 0.000 0.004 0.524 0.300 NA
#&gt; SRR1927025     5  0.3604      0.732 0.000 0.216 0.012 0.000 0.760 NA
#&gt; SRR1927023     5  0.1913      0.715 0.000 0.080 0.012 0.000 0.908 NA
#&gt; SRR1927022     1  0.3964      0.508 0.676 0.000 0.004 0.308 0.008 NA
#&gt; SRR1927021     5  0.4742      0.576 0.000 0.328 0.004 0.000 0.612 NA
#&gt; SRR1927020     4  0.3144      0.895 0.172 0.000 0.004 0.808 0.000 NA
#&gt; SRR1927019     2  0.1225      0.717 0.000 0.952 0.036 0.000 0.000 NA
#&gt; SRR1927071     4  0.2932      0.900 0.164 0.000 0.000 0.820 0.000 NA
#&gt; SRR1927069     2  0.3827      0.650 0.000 0.804 0.024 0.000 0.096 NA
#&gt; SRR1927070     1  0.1910      0.895 0.892 0.000 0.000 0.108 0.000 NA
#&gt; SRR1927068     4  0.3245      0.893 0.184 0.000 0.004 0.796 0.000 NA
#&gt; SRR1927066     4  0.2915      0.894 0.184 0.000 0.000 0.808 0.000 NA
#&gt; SRR1927065     2  0.3937     -0.394 0.000 0.572 0.424 0.000 0.004 NA
#&gt; SRR1927067     3  0.4372      0.490 0.000 0.432 0.544 0.000 0.000 NA
#&gt; SRR1927064     1  0.1405      0.906 0.948 0.000 0.004 0.024 0.000 NA
#&gt; SRR1927063     2  0.2355      0.651 0.000 0.876 0.112 0.000 0.004 NA
#&gt; SRR1927062     4  0.4994      0.603 0.364 0.000 0.036 0.576 0.000 NA
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-5-a').click(function(){
  $('#tab-MAD-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-signatures'>
<ul>
<li><a href='#tab-MAD-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-1-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-1"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-2-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-2"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-3-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-3"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-4-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-4"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-5-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-NMF-signature_compare](figure_cola/MAD-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-NMF-collect-classes](figure_cola/MAD-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:hclust*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "hclust"]
# you can also extract it by
# res = res_list["ATC:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16868 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 5.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-hclust-collect-plots](figure_cola/ATC-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-hclust-select-partition-number](figure_cola/ATC-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5073 0.493   0.493
#> 3 3 1.000           0.990       0.994         0.1964 0.898   0.794
#> 4 4 0.773           0.680       0.845         0.1475 0.879   0.692
#> 5 5 0.903           0.932       0.963         0.0927 0.879   0.612
#> 6 6 0.892           0.864       0.933         0.0113 0.989   0.955
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 5
#> attr(,"optional")
#> [1] 2 3
```

There is also optional best $k$ = 2 3 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-classes'>
<ul>
<li><a href='#tab-ATC-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-hclust-get-classes-1'>
<p><a id='tab-ATC-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1927048     1       0          1  1  0
#&gt; SRR1927061     2       0          1  0  1
#&gt; SRR1927060     1       0          1  1  0
#&gt; SRR1927059     2       0          1  0  1
#&gt; SRR1927058     1       0          1  1  0
#&gt; SRR1927057     2       0          1  0  1
#&gt; SRR1927055     2       0          1  0  1
#&gt; SRR1927056     1       0          1  1  0
#&gt; SRR1927054     1       0          1  1  0
#&gt; SRR1927052     1       0          1  1  0
#&gt; SRR1927053     2       0          1  0  1
#&gt; SRR1927051     2       0          1  0  1
#&gt; SRR1927050     1       0          1  1  0
#&gt; SRR1927049     2       0          1  0  1
#&gt; SRR1927047     2       0          1  0  1
#&gt; SRR1927046     1       0          1  1  0
#&gt; SRR1927045     2       0          1  0  1
#&gt; SRR1927044     1       0          1  1  0
#&gt; SRR1927043     2       0          1  0  1
#&gt; SRR1927042     1       0          1  1  0
#&gt; SRR1927040     1       0          1  1  0
#&gt; SRR1927039     2       0          1  0  1
#&gt; SRR1927038     1       0          1  1  0
#&gt; SRR1927037     2       0          1  0  1
#&gt; SRR1927036     1       0          1  1  0
#&gt; SRR1927035     2       0          1  0  1
#&gt; SRR1927034     1       0          1  1  0
#&gt; SRR1927033     2       0          1  0  1
#&gt; SRR1927032     1       0          1  1  0
#&gt; SRR1927031     2       0          1  0  1
#&gt; SRR1927030     1       0          1  1  0
#&gt; SRR1927028     1       0          1  1  0
#&gt; SRR1927029     2       0          1  0  1
#&gt; SRR1927027     1       0          1  1  0
#&gt; SRR1927026     1       0          1  1  0
#&gt; SRR1927024     1       0          1  1  0
#&gt; SRR1927025     2       0          1  0  1
#&gt; SRR1927023     2       0          1  0  1
#&gt; SRR1927022     1       0          1  1  0
#&gt; SRR1927021     2       0          1  0  1
#&gt; SRR1927020     1       0          1  1  0
#&gt; SRR1927019     2       0          1  0  1
#&gt; SRR1927071     1       0          1  1  0
#&gt; SRR1927069     2       0          1  0  1
#&gt; SRR1927070     1       0          1  1  0
#&gt; SRR1927068     1       0          1  1  0
#&gt; SRR1927066     1       0          1  1  0
#&gt; SRR1927065     2       0          1  0  1
#&gt; SRR1927067     2       0          1  0  1
#&gt; SRR1927064     1       0          1  1  0
#&gt; SRR1927063     2       0          1  0  1
#&gt; SRR1927062     1       0          1  1  0
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-1-a').click(function(){
  $('#tab-ATC-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-2'>
<p><a id='tab-ATC-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1    p2    p3
#&gt; SRR1927048     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1927061     3   0.348      0.884  0 0.128 0.872
#&gt; SRR1927060     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1927059     2   0.000      1.000  0 1.000 0.000
#&gt; SRR1927058     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1927057     2   0.000      1.000  0 1.000 0.000
#&gt; SRR1927055     3   0.000      0.960  0 0.000 1.000
#&gt; SRR1927056     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1927054     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1927052     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1927053     2   0.000      1.000  0 1.000 0.000
#&gt; SRR1927051     2   0.000      1.000  0 1.000 0.000
#&gt; SRR1927050     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1927049     2   0.000      1.000  0 1.000 0.000
#&gt; SRR1927047     2   0.000      1.000  0 1.000 0.000
#&gt; SRR1927046     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1927045     2   0.000      1.000  0 1.000 0.000
#&gt; SRR1927044     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1927043     3   0.129      0.954  0 0.032 0.968
#&gt; SRR1927042     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1927040     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1927039     2   0.000      1.000  0 1.000 0.000
#&gt; SRR1927038     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1927037     2   0.000      1.000  0 1.000 0.000
#&gt; SRR1927036     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1927035     2   0.000      1.000  0 1.000 0.000
#&gt; SRR1927034     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1927033     3   0.000      0.960  0 0.000 1.000
#&gt; SRR1927032     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1927031     2   0.000      1.000  0 1.000 0.000
#&gt; SRR1927030     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1927028     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1927029     3   0.129      0.954  0 0.032 0.968
#&gt; SRR1927027     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1927026     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1927024     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1927025     3   0.000      0.960  0 0.000 1.000
#&gt; SRR1927023     3   0.000      0.960  0 0.000 1.000
#&gt; SRR1927022     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1927021     2   0.000      1.000  0 1.000 0.000
#&gt; SRR1927020     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1927019     2   0.000      1.000  0 1.000 0.000
#&gt; SRR1927071     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1927069     2   0.000      1.000  0 1.000 0.000
#&gt; SRR1927070     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1927068     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1927066     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1927065     3   0.348      0.884  0 0.128 0.872
#&gt; SRR1927067     3   0.000      0.960  0 0.000 1.000
#&gt; SRR1927064     1   0.000      1.000  1 0.000 0.000
#&gt; SRR1927063     2   0.000      1.000  0 1.000 0.000
#&gt; SRR1927062     1   0.000      1.000  1 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-2-a').click(function(){
  $('#tab-ATC-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-3'>
<p><a id='tab-ATC-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1927048     1   0.000      0.697 1.000 0.000 0.000 0.000
#&gt; SRR1927061     3   0.276      0.834 0.000 0.128 0.872 0.000
#&gt; SRR1927060     1   0.000      0.697 1.000 0.000 0.000 0.000
#&gt; SRR1927059     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927058     1   0.000      0.697 1.000 0.000 0.000 0.000
#&gt; SRR1927057     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927055     3   0.112      0.891 0.000 0.000 0.964 0.036
#&gt; SRR1927056     4   0.485      0.978 0.400 0.000 0.000 0.600
#&gt; SRR1927054     1   0.000      0.697 1.000 0.000 0.000 0.000
#&gt; SRR1927052     1   0.500     -0.725 0.504 0.000 0.000 0.496
#&gt; SRR1927053     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927051     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927050     4   0.485      0.978 0.400 0.000 0.000 0.600
#&gt; SRR1927049     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927047     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927046     1   0.000      0.697 1.000 0.000 0.000 0.000
#&gt; SRR1927045     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927044     1   0.000      0.697 1.000 0.000 0.000 0.000
#&gt; SRR1927043     3   0.102      0.891 0.000 0.032 0.968 0.000
#&gt; SRR1927042     1   0.000      0.697 1.000 0.000 0.000 0.000
#&gt; SRR1927040     1   0.000      0.697 1.000 0.000 0.000 0.000
#&gt; SRR1927039     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927038     1   0.000      0.697 1.000 0.000 0.000 0.000
#&gt; SRR1927037     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927036     1   0.000      0.697 1.000 0.000 0.000 0.000
#&gt; SRR1927035     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927034     4   0.485      0.978 0.400 0.000 0.000 0.600
#&gt; SRR1927033     3   0.112      0.891 0.000 0.000 0.964 0.036
#&gt; SRR1927032     1   0.000      0.697 1.000 0.000 0.000 0.000
#&gt; SRR1927031     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927030     1   0.000      0.697 1.000 0.000 0.000 0.000
#&gt; SRR1927028     1   0.500     -0.725 0.504 0.000 0.000 0.496
#&gt; SRR1927029     3   0.102      0.891 0.000 0.032 0.968 0.000
#&gt; SRR1927027     4   0.499      0.820 0.472 0.000 0.000 0.528
#&gt; SRR1927026     4   0.485      0.978 0.400 0.000 0.000 0.600
#&gt; SRR1927024     1   0.500     -0.725 0.504 0.000 0.000 0.496
#&gt; SRR1927025     3   0.485      0.759 0.000 0.000 0.600 0.400
#&gt; SRR1927023     3   0.485      0.759 0.000 0.000 0.600 0.400
#&gt; SRR1927022     1   0.500     -0.708 0.512 0.000 0.000 0.488
#&gt; SRR1927021     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927020     4   0.485      0.978 0.400 0.000 0.000 0.600
#&gt; SRR1927019     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927071     1   0.500     -0.725 0.504 0.000 0.000 0.496
#&gt; SRR1927069     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927070     1   0.365      0.345 0.796 0.000 0.000 0.204
#&gt; SRR1927068     4   0.485      0.978 0.400 0.000 0.000 0.600
#&gt; SRR1927066     1   0.500     -0.725 0.504 0.000 0.000 0.496
#&gt; SRR1927065     3   0.276      0.834 0.000 0.128 0.872 0.000
#&gt; SRR1927067     3   0.000      0.891 0.000 0.000 1.000 0.000
#&gt; SRR1927064     1   0.000      0.697 1.000 0.000 0.000 0.000
#&gt; SRR1927063     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1927062     4   0.485      0.978 0.400 0.000 0.000 0.600
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-3-a').click(function(){
  $('#tab-ATC-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-4'>
<p><a id='tab-ATC-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1927048     1   0.000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927061     3   0.196      0.846 0.000 0.096 0.904 0.000 0.000
#&gt; SRR1927060     1   0.000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927059     2   0.000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927058     1   0.000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927057     2   0.000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927055     3   0.207      0.876 0.000 0.000 0.896 0.000 0.104
#&gt; SRR1927056     4   0.000      0.858 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927054     1   0.000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927052     4   0.269      0.853 0.156 0.000 0.000 0.844 0.000
#&gt; SRR1927053     2   0.000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927051     2   0.000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927050     4   0.000      0.858 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927049     2   0.000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927047     2   0.000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927046     1   0.000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927045     2   0.000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927044     1   0.000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927043     3   0.000      0.905 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927042     1   0.000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927040     1   0.000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927039     2   0.000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927038     1   0.000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927037     2   0.000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927036     1   0.000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927035     2   0.000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927034     4   0.000      0.858 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927033     3   0.207      0.876 0.000 0.000 0.896 0.000 0.104
#&gt; SRR1927032     1   0.000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927031     2   0.000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927030     1   0.000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927028     4   0.269      0.853 0.156 0.000 0.000 0.844 0.000
#&gt; SRR1927029     3   0.000      0.905 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927027     4   0.191      0.855 0.092 0.000 0.000 0.908 0.000
#&gt; SRR1927026     4   0.000      0.858 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927024     4   0.269      0.853 0.156 0.000 0.000 0.844 0.000
#&gt; SRR1927025     5   0.000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1927023     5   0.000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1927022     4   0.285      0.839 0.172 0.000 0.000 0.828 0.000
#&gt; SRR1927021     2   0.000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927020     4   0.000      0.858 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927019     2   0.000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927071     4   0.269      0.853 0.156 0.000 0.000 0.844 0.000
#&gt; SRR1927069     2   0.000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927070     4   0.429      0.324 0.464 0.000 0.000 0.536 0.000
#&gt; SRR1927068     4   0.000      0.858 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927066     4   0.269      0.853 0.156 0.000 0.000 0.844 0.000
#&gt; SRR1927065     3   0.196      0.846 0.000 0.096 0.904 0.000 0.000
#&gt; SRR1927067     3   0.088      0.904 0.000 0.000 0.968 0.000 0.032
#&gt; SRR1927064     1   0.000      1.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927063     2   0.000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927062     4   0.000      0.858 0.000 0.000 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-4-a').click(function(){
  $('#tab-ATC-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-5'>
<p><a id='tab-ATC-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1927048     1   0.000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927061     3   0.525     0.7611 0.000 0.096 0.488 0.000 0.416 0.000
#&gt; SRR1927060     1   0.000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927059     2   0.000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927058     1   0.000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927057     2   0.000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927055     3   0.000     0.6059 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927056     4   0.000     0.7524 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927054     1   0.000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927052     4   0.242     0.7453 0.156 0.000 0.000 0.844 0.000 0.000
#&gt; SRR1927053     2   0.000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927051     2   0.000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927050     4   0.000     0.7524 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927049     2   0.000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927047     2   0.000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927046     1   0.000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927045     2   0.000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927044     1   0.000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927043     3   0.379     0.8052 0.000 0.000 0.584 0.000 0.416 0.000
#&gt; SRR1927042     1   0.000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927040     1   0.000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927039     2   0.000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927038     1   0.000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927037     2   0.000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927036     1   0.000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927035     2   0.000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927034     4   0.000     0.7524 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927033     3   0.000     0.6059 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927032     1   0.000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927031     2   0.000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927030     1   0.000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927028     4   0.242     0.7453 0.156 0.000 0.000 0.844 0.000 0.000
#&gt; SRR1927029     3   0.379     0.8052 0.000 0.000 0.584 0.000 0.416 0.000
#&gt; SRR1927027     6   0.466     0.0000 0.052 0.000 0.000 0.364 0.000 0.584
#&gt; SRR1927026     4   0.000     0.7524 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927024     4   0.242     0.7453 0.156 0.000 0.000 0.844 0.000 0.000
#&gt; SRR1927025     5   0.379     1.0000 0.000 0.000 0.000 0.000 0.584 0.416
#&gt; SRR1927023     5   0.379     1.0000 0.000 0.000 0.000 0.000 0.584 0.416
#&gt; SRR1927022     4   0.256     0.7197 0.172 0.000 0.000 0.828 0.000 0.000
#&gt; SRR1927021     2   0.000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927020     4   0.000     0.7524 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927019     2   0.000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927071     4   0.242     0.7453 0.156 0.000 0.000 0.844 0.000 0.000
#&gt; SRR1927069     2   0.000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927070     4   0.385     0.0649 0.464 0.000 0.000 0.536 0.000 0.000
#&gt; SRR1927068     4   0.000     0.7524 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927066     4   0.242     0.7453 0.156 0.000 0.000 0.844 0.000 0.000
#&gt; SRR1927065     3   0.525     0.7611 0.000 0.096 0.488 0.000 0.416 0.000
#&gt; SRR1927067     3   0.371     0.8025 0.000 0.000 0.620 0.000 0.380 0.000
#&gt; SRR1927064     1   0.000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927063     2   0.000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927062     4   0.000     0.7524 0.000 0.000 0.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-5-a').click(function(){
  $('#tab-ATC-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-signatures'>
<ul>
<li><a href='#tab-ATC-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-1-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-1"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-2-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-2"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-3-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-3"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-4-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-4"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-5-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-hclust-signature_compare](figure_cola/ATC-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-hclust-collect-classes](figure_cola/ATC-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:kmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "kmeans"]
# you can also extract it by
# res = res_list["ATC:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16868 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-kmeans-collect-plots](figure_cola/ATC-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-kmeans-select-partition-number](figure_cola/ATC-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5072 0.493   0.493
#> 3 3 0.744           0.794       0.791         0.2559 0.798   0.607
#> 4 4 0.700           0.915       0.848         0.1253 0.889   0.678
#> 5 5 0.754           0.843       0.841         0.0692 0.949   0.796
#> 6 6 0.848           0.776       0.836         0.0509 0.962   0.827
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-classes'>
<ul>
<li><a href='#tab-ATC-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-kmeans-get-classes-1'>
<p><a id='tab-ATC-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1927048     1  0.0000      1.000 1.000 0.000
#&gt; SRR1927061     2  0.0000      0.999 0.000 1.000
#&gt; SRR1927060     1  0.0000      1.000 1.000 0.000
#&gt; SRR1927059     2  0.0000      0.999 0.000 1.000
#&gt; SRR1927058     1  0.0000      1.000 1.000 0.000
#&gt; SRR1927057     2  0.0000      0.999 0.000 1.000
#&gt; SRR1927055     2  0.0938      0.988 0.012 0.988
#&gt; SRR1927056     1  0.0000      1.000 1.000 0.000
#&gt; SRR1927054     1  0.0000      1.000 1.000 0.000
#&gt; SRR1927052     1  0.0000      1.000 1.000 0.000
#&gt; SRR1927053     2  0.0000      0.999 0.000 1.000
#&gt; SRR1927051     2  0.0000      0.999 0.000 1.000
#&gt; SRR1927050     1  0.0000      1.000 1.000 0.000
#&gt; SRR1927049     2  0.0000      0.999 0.000 1.000
#&gt; SRR1927047     2  0.0000      0.999 0.000 1.000
#&gt; SRR1927046     1  0.0000      1.000 1.000 0.000
#&gt; SRR1927045     2  0.0000      0.999 0.000 1.000
#&gt; SRR1927044     1  0.0000      1.000 1.000 0.000
#&gt; SRR1927043     2  0.0000      0.999 0.000 1.000
#&gt; SRR1927042     1  0.0000      1.000 1.000 0.000
#&gt; SRR1927040     1  0.0000      1.000 1.000 0.000
#&gt; SRR1927039     2  0.0000      0.999 0.000 1.000
#&gt; SRR1927038     1  0.0000      1.000 1.000 0.000
#&gt; SRR1927037     2  0.0000      0.999 0.000 1.000
#&gt; SRR1927036     1  0.0000      1.000 1.000 0.000
#&gt; SRR1927035     2  0.0000      0.999 0.000 1.000
#&gt; SRR1927034     1  0.0000      1.000 1.000 0.000
#&gt; SRR1927033     2  0.0000      0.999 0.000 1.000
#&gt; SRR1927032     1  0.0000      1.000 1.000 0.000
#&gt; SRR1927031     2  0.0000      0.999 0.000 1.000
#&gt; SRR1927030     1  0.0000      1.000 1.000 0.000
#&gt; SRR1927028     1  0.0000      1.000 1.000 0.000
#&gt; SRR1927029     2  0.0000      0.999 0.000 1.000
#&gt; SRR1927027     1  0.0000      1.000 1.000 0.000
#&gt; SRR1927026     1  0.0000      1.000 1.000 0.000
#&gt; SRR1927024     1  0.0000      1.000 1.000 0.000
#&gt; SRR1927025     2  0.0000      0.999 0.000 1.000
#&gt; SRR1927023     2  0.0000      0.999 0.000 1.000
#&gt; SRR1927022     1  0.0000      1.000 1.000 0.000
#&gt; SRR1927021     2  0.0000      0.999 0.000 1.000
#&gt; SRR1927020     1  0.0000      1.000 1.000 0.000
#&gt; SRR1927019     2  0.0000      0.999 0.000 1.000
#&gt; SRR1927071     1  0.0000      1.000 1.000 0.000
#&gt; SRR1927069     2  0.0000      0.999 0.000 1.000
#&gt; SRR1927070     1  0.0000      1.000 1.000 0.000
#&gt; SRR1927068     1  0.0000      1.000 1.000 0.000
#&gt; SRR1927066     1  0.0000      1.000 1.000 0.000
#&gt; SRR1927065     2  0.0000      0.999 0.000 1.000
#&gt; SRR1927067     2  0.0000      0.999 0.000 1.000
#&gt; SRR1927064     1  0.0000      1.000 1.000 0.000
#&gt; SRR1927063     2  0.0000      0.999 0.000 1.000
#&gt; SRR1927062     1  0.0000      1.000 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-1-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-2'>
<p><a id='tab-ATC-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1927048     1   0.000      0.982 1.000 0.000 0.000
#&gt; SRR1927061     2   0.603      0.718 0.000 0.624 0.376
#&gt; SRR1927060     1   0.000      0.982 1.000 0.000 0.000
#&gt; SRR1927059     2   0.000      0.874 0.000 1.000 0.000
#&gt; SRR1927058     1   0.000      0.982 1.000 0.000 0.000
#&gt; SRR1927057     2   0.000      0.874 0.000 1.000 0.000
#&gt; SRR1927055     3   0.945     -0.522 0.180 0.388 0.432
#&gt; SRR1927056     3   0.622      0.776 0.432 0.000 0.568
#&gt; SRR1927054     1   0.000      0.982 1.000 0.000 0.000
#&gt; SRR1927052     3   0.622      0.776 0.432 0.000 0.568
#&gt; SRR1927053     2   0.000      0.874 0.000 1.000 0.000
#&gt; SRR1927051     2   0.000      0.874 0.000 1.000 0.000
#&gt; SRR1927050     3   0.622      0.776 0.432 0.000 0.568
#&gt; SRR1927049     2   0.000      0.874 0.000 1.000 0.000
#&gt; SRR1927047     2   0.000      0.874 0.000 1.000 0.000
#&gt; SRR1927046     1   0.000      0.982 1.000 0.000 0.000
#&gt; SRR1927045     2   0.000      0.874 0.000 1.000 0.000
#&gt; SRR1927044     1   0.000      0.982 1.000 0.000 0.000
#&gt; SRR1927043     2   0.622      0.693 0.000 0.568 0.432
#&gt; SRR1927042     1   0.000      0.982 1.000 0.000 0.000
#&gt; SRR1927040     1   0.000      0.982 1.000 0.000 0.000
#&gt; SRR1927039     2   0.000      0.874 0.000 1.000 0.000
#&gt; SRR1927038     1   0.000      0.982 1.000 0.000 0.000
#&gt; SRR1927037     2   0.000      0.874 0.000 1.000 0.000
#&gt; SRR1927036     1   0.000      0.982 1.000 0.000 0.000
#&gt; SRR1927035     2   0.000      0.874 0.000 1.000 0.000
#&gt; SRR1927034     3   0.622      0.776 0.432 0.000 0.568
#&gt; SRR1927033     2   0.622      0.693 0.000 0.568 0.432
#&gt; SRR1927032     1   0.000      0.982 1.000 0.000 0.000
#&gt; SRR1927031     2   0.000      0.874 0.000 1.000 0.000
#&gt; SRR1927030     1   0.000      0.982 1.000 0.000 0.000
#&gt; SRR1927028     3   0.622      0.776 0.432 0.000 0.568
#&gt; SRR1927029     2   0.622      0.693 0.000 0.568 0.432
#&gt; SRR1927027     3   0.623      0.769 0.436 0.000 0.564
#&gt; SRR1927026     3   0.622      0.776 0.432 0.000 0.568
#&gt; SRR1927024     3   0.622      0.776 0.432 0.000 0.568
#&gt; SRR1927025     2   0.622      0.693 0.000 0.568 0.432
#&gt; SRR1927023     3   0.945     -0.522 0.180 0.388 0.432
#&gt; SRR1927022     3   0.624      0.762 0.440 0.000 0.560
#&gt; SRR1927021     2   0.000      0.874 0.000 1.000 0.000
#&gt; SRR1927020     3   0.622      0.776 0.432 0.000 0.568
#&gt; SRR1927019     2   0.000      0.874 0.000 1.000 0.000
#&gt; SRR1927071     3   0.622      0.776 0.432 0.000 0.568
#&gt; SRR1927069     2   0.000      0.874 0.000 1.000 0.000
#&gt; SRR1927070     1   0.355      0.720 0.868 0.000 0.132
#&gt; SRR1927068     3   0.622      0.776 0.432 0.000 0.568
#&gt; SRR1927066     3   0.622      0.776 0.432 0.000 0.568
#&gt; SRR1927065     2   0.622      0.693 0.000 0.568 0.432
#&gt; SRR1927067     2   0.622      0.693 0.000 0.568 0.432
#&gt; SRR1927064     1   0.000      0.982 1.000 0.000 0.000
#&gt; SRR1927063     2   0.000      0.874 0.000 1.000 0.000
#&gt; SRR1927062     3   0.622      0.776 0.432 0.000 0.568
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-2-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-3'>
<p><a id='tab-ATC-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1927048     1  0.3942      0.951 0.764 0.000 0.000 0.236
#&gt; SRR1927061     3  0.5496      0.804 0.036 0.312 0.652 0.000
#&gt; SRR1927060     1  0.3942      0.951 0.764 0.000 0.000 0.236
#&gt; SRR1927059     2  0.1637      0.963 0.060 0.940 0.000 0.000
#&gt; SRR1927058     1  0.4477      0.914 0.688 0.000 0.000 0.312
#&gt; SRR1927057     2  0.1792      0.952 0.068 0.932 0.000 0.000
#&gt; SRR1927055     3  0.4948      0.857 0.100 0.124 0.776 0.000
#&gt; SRR1927056     4  0.3726      0.872 0.000 0.000 0.212 0.788
#&gt; SRR1927054     1  0.3942      0.951 0.764 0.000 0.000 0.236
#&gt; SRR1927052     4  0.0188      0.880 0.004 0.000 0.000 0.996
#&gt; SRR1927053     2  0.1474      0.962 0.052 0.948 0.000 0.000
#&gt; SRR1927051     2  0.0336      0.970 0.008 0.992 0.000 0.000
#&gt; SRR1927050     4  0.3726      0.872 0.000 0.000 0.212 0.788
#&gt; SRR1927049     2  0.0336      0.970 0.008 0.992 0.000 0.000
#&gt; SRR1927047     2  0.0817      0.970 0.024 0.976 0.000 0.000
#&gt; SRR1927046     1  0.3942      0.951 0.764 0.000 0.000 0.236
#&gt; SRR1927045     2  0.0817      0.961 0.024 0.976 0.000 0.000
#&gt; SRR1927044     1  0.4477      0.914 0.688 0.000 0.000 0.312
#&gt; SRR1927043     3  0.4175      0.920 0.012 0.212 0.776 0.000
#&gt; SRR1927042     1  0.3942      0.951 0.764 0.000 0.000 0.236
#&gt; SRR1927040     1  0.3942      0.951 0.764 0.000 0.000 0.236
#&gt; SRR1927039     2  0.1474      0.962 0.052 0.948 0.000 0.000
#&gt; SRR1927038     1  0.3942      0.951 0.764 0.000 0.000 0.236
#&gt; SRR1927037     2  0.1302      0.964 0.044 0.956 0.000 0.000
#&gt; SRR1927036     1  0.4477      0.914 0.688 0.000 0.000 0.312
#&gt; SRR1927035     2  0.0188      0.971 0.004 0.996 0.000 0.000
#&gt; SRR1927034     4  0.3726      0.872 0.000 0.000 0.212 0.788
#&gt; SRR1927033     3  0.4049      0.920 0.008 0.212 0.780 0.000
#&gt; SRR1927032     1  0.3942      0.951 0.764 0.000 0.000 0.236
#&gt; SRR1927031     2  0.1940      0.950 0.076 0.924 0.000 0.000
#&gt; SRR1927030     1  0.4477      0.914 0.688 0.000 0.000 0.312
#&gt; SRR1927028     4  0.0000      0.883 0.000 0.000 0.000 1.000
#&gt; SRR1927029     3  0.4175      0.920 0.012 0.212 0.776 0.000
#&gt; SRR1927027     4  0.4487      0.813 0.092 0.000 0.100 0.808
#&gt; SRR1927026     4  0.2281      0.886 0.000 0.000 0.096 0.904
#&gt; SRR1927024     4  0.0000      0.883 0.000 0.000 0.000 1.000
#&gt; SRR1927025     3  0.5998      0.883 0.108 0.212 0.680 0.000
#&gt; SRR1927023     3  0.6327      0.811 0.228 0.124 0.648 0.000
#&gt; SRR1927022     4  0.0336      0.877 0.008 0.000 0.000 0.992
#&gt; SRR1927021     2  0.0336      0.970 0.008 0.992 0.000 0.000
#&gt; SRR1927020     4  0.3726      0.872 0.000 0.000 0.212 0.788
#&gt; SRR1927019     2  0.0336      0.970 0.008 0.992 0.000 0.000
#&gt; SRR1927071     4  0.0000      0.883 0.000 0.000 0.000 1.000
#&gt; SRR1927069     2  0.0336      0.971 0.008 0.992 0.000 0.000
#&gt; SRR1927070     1  0.4961      0.730 0.552 0.000 0.000 0.448
#&gt; SRR1927068     4  0.3726      0.872 0.000 0.000 0.212 0.788
#&gt; SRR1927066     4  0.0000      0.883 0.000 0.000 0.000 1.000
#&gt; SRR1927065     3  0.4781      0.913 0.036 0.212 0.752 0.000
#&gt; SRR1927067     3  0.3726      0.920 0.000 0.212 0.788 0.000
#&gt; SRR1927064     1  0.3942      0.951 0.764 0.000 0.000 0.236
#&gt; SRR1927063     2  0.0336      0.970 0.008 0.992 0.000 0.000
#&gt; SRR1927062     4  0.2589      0.884 0.000 0.000 0.116 0.884
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-3-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-4'>
<p><a id='tab-ATC-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1927048     1  0.0000     0.9828 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927061     3  0.4031     0.8146 0.000 0.124 0.804 0.008 0.064
#&gt; SRR1927060     1  0.0000     0.9828 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.2471     0.9123 0.000 0.864 0.000 0.000 0.136
#&gt; SRR1927058     1  0.0992     0.9671 0.968 0.000 0.024 0.000 0.008
#&gt; SRR1927057     2  0.3109     0.8880 0.000 0.800 0.000 0.000 0.200
#&gt; SRR1927055     3  0.2511     0.8994 0.000 0.024 0.908 0.024 0.044
#&gt; SRR1927056     4  0.2773     0.7611 0.164 0.000 0.000 0.836 0.000
#&gt; SRR1927054     1  0.0000     0.9828 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927052     5  0.6133     0.8315 0.164 0.000 0.000 0.292 0.544
#&gt; SRR1927053     2  0.2953     0.9090 0.000 0.844 0.000 0.012 0.144
#&gt; SRR1927051     2  0.0162     0.9340 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1927050     4  0.2773     0.7611 0.164 0.000 0.000 0.836 0.000
#&gt; SRR1927049     2  0.0162     0.9340 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1927047     2  0.1106     0.9337 0.000 0.964 0.000 0.012 0.024
#&gt; SRR1927046     1  0.0000     0.9828 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927045     2  0.1478     0.9147 0.000 0.936 0.000 0.000 0.064
#&gt; SRR1927044     1  0.1741     0.9387 0.936 0.000 0.024 0.000 0.040
#&gt; SRR1927043     3  0.1153     0.9076 0.000 0.024 0.964 0.008 0.004
#&gt; SRR1927042     1  0.0000     0.9828 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0000     0.9828 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927039     2  0.2953     0.9090 0.000 0.844 0.000 0.012 0.144
#&gt; SRR1927038     1  0.0000     0.9828 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.2516     0.9117 0.000 0.860 0.000 0.000 0.140
#&gt; SRR1927036     1  0.0992     0.9671 0.968 0.000 0.024 0.000 0.008
#&gt; SRR1927035     2  0.0404     0.9354 0.000 0.988 0.000 0.000 0.012
#&gt; SRR1927034     4  0.2773     0.7611 0.164 0.000 0.000 0.836 0.000
#&gt; SRR1927033     3  0.2095     0.9036 0.000 0.024 0.928 0.020 0.028
#&gt; SRR1927032     1  0.0000     0.9828 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927031     2  0.3109     0.8880 0.000 0.800 0.000 0.000 0.200
#&gt; SRR1927030     1  0.1741     0.9387 0.936 0.000 0.024 0.000 0.040
#&gt; SRR1927028     5  0.6133     0.8315 0.164 0.000 0.000 0.292 0.544
#&gt; SRR1927029     3  0.1153     0.9076 0.000 0.024 0.964 0.008 0.004
#&gt; SRR1927027     4  0.5697    -0.0088 0.092 0.000 0.000 0.548 0.360
#&gt; SRR1927026     4  0.6101     0.1729 0.164 0.000 0.000 0.552 0.284
#&gt; SRR1927024     5  0.6133     0.8315 0.164 0.000 0.000 0.292 0.544
#&gt; SRR1927025     3  0.5017     0.8143 0.000 0.024 0.736 0.076 0.164
#&gt; SRR1927023     3  0.6047     0.7524 0.000 0.024 0.628 0.120 0.228
#&gt; SRR1927022     5  0.6133     0.8315 0.164 0.000 0.000 0.292 0.544
#&gt; SRR1927021     2  0.0162     0.9340 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1927020     4  0.2773     0.7611 0.164 0.000 0.000 0.836 0.000
#&gt; SRR1927019     2  0.0162     0.9340 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1927071     5  0.6133     0.8315 0.164 0.000 0.000 0.292 0.544
#&gt; SRR1927069     2  0.0807     0.9334 0.000 0.976 0.000 0.012 0.012
#&gt; SRR1927070     5  0.4897     0.2870 0.460 0.000 0.024 0.000 0.516
#&gt; SRR1927068     4  0.2773     0.7611 0.164 0.000 0.000 0.836 0.000
#&gt; SRR1927066     5  0.6133     0.8315 0.164 0.000 0.000 0.292 0.544
#&gt; SRR1927065     3  0.2390     0.8926 0.000 0.024 0.908 0.008 0.060
#&gt; SRR1927067     3  0.0703     0.9076 0.000 0.024 0.976 0.000 0.000
#&gt; SRR1927064     1  0.0000     0.9828 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927063     2  0.0162     0.9340 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1927062     4  0.5864     0.3425 0.164 0.000 0.000 0.600 0.236
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-4-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-5'>
<p><a id='tab-ATC-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1927048     1  0.0972    0.91142 0.964 0.000 0.008 0.000 0.028 0.000
#&gt; SRR1927061     3  0.2701    0.74686 0.000 0.044 0.884 0.000 0.028 0.044
#&gt; SRR1927060     1  0.0146    0.91691 0.996 0.000 0.000 0.000 0.004 0.000
#&gt; SRR1927059     2  0.3776    0.83369 0.000 0.756 0.000 0.000 0.048 0.196
#&gt; SRR1927058     1  0.2933    0.83043 0.796 0.000 0.000 0.004 0.200 0.000
#&gt; SRR1927057     2  0.4632    0.78932 0.000 0.668 0.000 0.004 0.072 0.256
#&gt; SRR1927055     3  0.3534    0.71082 0.000 0.008 0.828 0.020 0.108 0.036
#&gt; SRR1927056     6  0.4270    1.00000 0.052 0.000 0.000 0.264 0.000 0.684
#&gt; SRR1927054     1  0.0146    0.91691 0.996 0.000 0.000 0.000 0.004 0.000
#&gt; SRR1927052     4  0.1524    0.69275 0.060 0.000 0.000 0.932 0.008 0.000
#&gt; SRR1927053     2  0.4024    0.83264 0.000 0.748 0.000 0.008 0.048 0.196
#&gt; SRR1927051     2  0.0291    0.87628 0.000 0.992 0.000 0.000 0.004 0.004
#&gt; SRR1927050     6  0.4270    1.00000 0.052 0.000 0.000 0.264 0.000 0.684
#&gt; SRR1927049     2  0.0146    0.87632 0.000 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1927047     2  0.1546    0.87832 0.000 0.944 0.000 0.020 0.016 0.020
#&gt; SRR1927046     1  0.0972    0.91142 0.964 0.000 0.008 0.000 0.028 0.000
#&gt; SRR1927045     2  0.2113    0.84360 0.000 0.908 0.000 0.004 0.028 0.060
#&gt; SRR1927044     1  0.3612    0.80566 0.764 0.000 0.000 0.036 0.200 0.000
#&gt; SRR1927043     3  0.0260    0.85221 0.000 0.008 0.992 0.000 0.000 0.000
#&gt; SRR1927042     1  0.0000    0.91682 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0146    0.91691 0.996 0.000 0.000 0.000 0.004 0.000
#&gt; SRR1927039     2  0.3835    0.83135 0.000 0.748 0.000 0.000 0.048 0.204
#&gt; SRR1927038     1  0.0146    0.91691 0.996 0.000 0.000 0.000 0.004 0.000
#&gt; SRR1927037     2  0.3744    0.83436 0.000 0.756 0.000 0.000 0.044 0.200
#&gt; SRR1927036     1  0.2933    0.83043 0.796 0.000 0.000 0.004 0.200 0.000
#&gt; SRR1927035     2  0.0547    0.87967 0.000 0.980 0.000 0.000 0.000 0.020
#&gt; SRR1927034     6  0.4270    1.00000 0.052 0.000 0.000 0.264 0.000 0.684
#&gt; SRR1927033     3  0.2849    0.78642 0.000 0.008 0.880 0.020 0.056 0.036
#&gt; SRR1927032     1  0.0972    0.91142 0.964 0.000 0.008 0.000 0.028 0.000
#&gt; SRR1927031     2  0.4681    0.78799 0.000 0.664 0.000 0.004 0.076 0.256
#&gt; SRR1927030     1  0.3612    0.80566 0.764 0.000 0.000 0.036 0.200 0.000
#&gt; SRR1927028     4  0.1141    0.69503 0.052 0.000 0.000 0.948 0.000 0.000
#&gt; SRR1927029     3  0.0260    0.85221 0.000 0.008 0.992 0.000 0.000 0.000
#&gt; SRR1927027     4  0.6232   -0.00807 0.028 0.000 0.000 0.500 0.184 0.288
#&gt; SRR1927026     4  0.4508    0.07382 0.052 0.000 0.000 0.632 0.000 0.316
#&gt; SRR1927024     4  0.1500    0.69344 0.052 0.000 0.000 0.936 0.012 0.000
#&gt; SRR1927025     5  0.4097    0.64755 0.000 0.008 0.488 0.000 0.504 0.000
#&gt; SRR1927023     5  0.3774    0.71944 0.000 0.008 0.328 0.000 0.664 0.000
#&gt; SRR1927022     4  0.2318    0.67478 0.064 0.000 0.000 0.892 0.044 0.000
#&gt; SRR1927021     2  0.0717    0.87513 0.000 0.976 0.000 0.016 0.008 0.000
#&gt; SRR1927020     6  0.4270    1.00000 0.052 0.000 0.000 0.264 0.000 0.684
#&gt; SRR1927019     2  0.0146    0.87632 0.000 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1927071     4  0.1141    0.69503 0.052 0.000 0.000 0.948 0.000 0.000
#&gt; SRR1927069     2  0.1714    0.87717 0.000 0.936 0.000 0.024 0.016 0.024
#&gt; SRR1927070     4  0.5890    0.09621 0.340 0.000 0.000 0.448 0.212 0.000
#&gt; SRR1927068     6  0.4270    1.00000 0.052 0.000 0.000 0.264 0.000 0.684
#&gt; SRR1927066     4  0.1141    0.69503 0.052 0.000 0.000 0.948 0.000 0.000
#&gt; SRR1927065     3  0.1970    0.80183 0.000 0.008 0.920 0.000 0.028 0.044
#&gt; SRR1927067     3  0.1124    0.84010 0.000 0.008 0.956 0.000 0.036 0.000
#&gt; SRR1927064     1  0.0972    0.91142 0.964 0.000 0.008 0.000 0.028 0.000
#&gt; SRR1927063     2  0.0291    0.87678 0.000 0.992 0.000 0.000 0.004 0.004
#&gt; SRR1927062     4  0.4712   -0.18646 0.052 0.000 0.000 0.564 0.000 0.384
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-5-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-signatures'>
<ul>
<li><a href='#tab-ATC-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-kmeans-signature_compare](figure_cola/ATC-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-kmeans-collect-classes](figure_cola/ATC-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:skmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "skmeans"]
# you can also extract it by
# res = res_list["ATC:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16868 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-skmeans-collect-plots](figure_cola/ATC-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-skmeans-select-partition-number](figure_cola/ATC-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5073 0.493   0.493
#> 3 3 1.000           0.980       0.990         0.2886 0.853   0.702
#> 4 4 0.946           0.868       0.955         0.1126 0.928   0.793
#> 5 5 0.957           0.930       0.970         0.0308 0.967   0.881
#> 6 6 0.953           0.917       0.957         0.0312 0.968   0.875
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2 3 4 5
```

There is also optional best $k$ = 2 3 4 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-classes'>
<ul>
<li><a href='#tab-ATC-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-skmeans-get-classes-1'>
<p><a id='tab-ATC-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1927048     1       0          1  1  0
#&gt; SRR1927061     2       0          1  0  1
#&gt; SRR1927060     1       0          1  1  0
#&gt; SRR1927059     2       0          1  0  1
#&gt; SRR1927058     1       0          1  1  0
#&gt; SRR1927057     2       0          1  0  1
#&gt; SRR1927055     2       0          1  0  1
#&gt; SRR1927056     1       0          1  1  0
#&gt; SRR1927054     1       0          1  1  0
#&gt; SRR1927052     1       0          1  1  0
#&gt; SRR1927053     2       0          1  0  1
#&gt; SRR1927051     2       0          1  0  1
#&gt; SRR1927050     1       0          1  1  0
#&gt; SRR1927049     2       0          1  0  1
#&gt; SRR1927047     2       0          1  0  1
#&gt; SRR1927046     1       0          1  1  0
#&gt; SRR1927045     2       0          1  0  1
#&gt; SRR1927044     1       0          1  1  0
#&gt; SRR1927043     2       0          1  0  1
#&gt; SRR1927042     1       0          1  1  0
#&gt; SRR1927040     1       0          1  1  0
#&gt; SRR1927039     2       0          1  0  1
#&gt; SRR1927038     1       0          1  1  0
#&gt; SRR1927037     2       0          1  0  1
#&gt; SRR1927036     1       0          1  1  0
#&gt; SRR1927035     2       0          1  0  1
#&gt; SRR1927034     1       0          1  1  0
#&gt; SRR1927033     2       0          1  0  1
#&gt; SRR1927032     1       0          1  1  0
#&gt; SRR1927031     2       0          1  0  1
#&gt; SRR1927030     1       0          1  1  0
#&gt; SRR1927028     1       0          1  1  0
#&gt; SRR1927029     2       0          1  0  1
#&gt; SRR1927027     1       0          1  1  0
#&gt; SRR1927026     1       0          1  1  0
#&gt; SRR1927024     1       0          1  1  0
#&gt; SRR1927025     2       0          1  0  1
#&gt; SRR1927023     2       0          1  0  1
#&gt; SRR1927022     1       0          1  1  0
#&gt; SRR1927021     2       0          1  0  1
#&gt; SRR1927020     1       0          1  1  0
#&gt; SRR1927019     2       0          1  0  1
#&gt; SRR1927071     1       0          1  1  0
#&gt; SRR1927069     2       0          1  0  1
#&gt; SRR1927070     1       0          1  1  0
#&gt; SRR1927068     1       0          1  1  0
#&gt; SRR1927066     1       0          1  1  0
#&gt; SRR1927065     2       0          1  0  1
#&gt; SRR1927067     2       0          1  0  1
#&gt; SRR1927064     1       0          1  1  0
#&gt; SRR1927063     2       0          1  0  1
#&gt; SRR1927062     1       0          1  1  0
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-1-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-2'>
<p><a id='tab-ATC-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1927048     3  0.0424      0.998 0.008 0.000 0.992
#&gt; SRR1927061     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927060     3  0.0424      0.998 0.008 0.000 0.992
#&gt; SRR1927059     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927058     3  0.0424      0.998 0.008 0.000 0.992
#&gt; SRR1927057     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927055     2  0.0424      0.995 0.000 0.992 0.008
#&gt; SRR1927056     1  0.0000      0.973 1.000 0.000 0.000
#&gt; SRR1927054     3  0.0424      0.998 0.008 0.000 0.992
#&gt; SRR1927052     1  0.0000      0.973 1.000 0.000 0.000
#&gt; SRR1927053     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927051     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927050     1  0.0000      0.973 1.000 0.000 0.000
#&gt; SRR1927049     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927047     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927046     3  0.0424      0.998 0.008 0.000 0.992
#&gt; SRR1927045     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927044     3  0.0747      0.993 0.016 0.000 0.984
#&gt; SRR1927043     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927042     3  0.0424      0.998 0.008 0.000 0.992
#&gt; SRR1927040     3  0.0424      0.998 0.008 0.000 0.992
#&gt; SRR1927039     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927038     3  0.0424      0.998 0.008 0.000 0.992
#&gt; SRR1927037     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927036     3  0.0747      0.993 0.016 0.000 0.984
#&gt; SRR1927035     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927034     1  0.0000      0.973 1.000 0.000 0.000
#&gt; SRR1927033     2  0.0424      0.995 0.000 0.992 0.008
#&gt; SRR1927032     3  0.0424      0.998 0.008 0.000 0.992
#&gt; SRR1927031     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927030     3  0.0747      0.993 0.016 0.000 0.984
#&gt; SRR1927028     1  0.0000      0.973 1.000 0.000 0.000
#&gt; SRR1927029     2  0.0237      0.997 0.000 0.996 0.004
#&gt; SRR1927027     1  0.0000      0.973 1.000 0.000 0.000
#&gt; SRR1927026     1  0.0000      0.973 1.000 0.000 0.000
#&gt; SRR1927024     1  0.0000      0.973 1.000 0.000 0.000
#&gt; SRR1927025     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927023     2  0.0237      0.997 0.000 0.996 0.004
#&gt; SRR1927022     1  0.0000      0.973 1.000 0.000 0.000
#&gt; SRR1927021     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927020     1  0.0000      0.973 1.000 0.000 0.000
#&gt; SRR1927019     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927071     1  0.0000      0.973 1.000 0.000 0.000
#&gt; SRR1927069     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927070     1  0.5988      0.407 0.632 0.000 0.368
#&gt; SRR1927068     1  0.0000      0.973 1.000 0.000 0.000
#&gt; SRR1927066     1  0.0000      0.973 1.000 0.000 0.000
#&gt; SRR1927065     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927067     2  0.0237      0.997 0.000 0.996 0.004
#&gt; SRR1927064     3  0.0424      0.998 0.008 0.000 0.992
#&gt; SRR1927063     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1927062     1  0.0000      0.973 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-2-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-3'>
<p><a id='tab-ATC-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1927048     1   0.000      0.986 1.000 0.000 0.000 0.000
#&gt; SRR1927061     2   0.179      0.859 0.000 0.932 0.068 0.000
#&gt; SRR1927060     1   0.000      0.986 1.000 0.000 0.000 0.000
#&gt; SRR1927059     2   0.000      0.924 0.000 1.000 0.000 0.000
#&gt; SRR1927058     1   0.000      0.986 1.000 0.000 0.000 0.000
#&gt; SRR1927057     2   0.000      0.924 0.000 1.000 0.000 0.000
#&gt; SRR1927055     3   0.000      0.784 0.000 0.000 1.000 0.000
#&gt; SRR1927056     4   0.000      0.970 0.000 0.000 0.000 1.000
#&gt; SRR1927054     1   0.000      0.986 1.000 0.000 0.000 0.000
#&gt; SRR1927052     4   0.000      0.970 0.000 0.000 0.000 1.000
#&gt; SRR1927053     2   0.000      0.924 0.000 1.000 0.000 0.000
#&gt; SRR1927051     2   0.000      0.924 0.000 1.000 0.000 0.000
#&gt; SRR1927050     4   0.000      0.970 0.000 0.000 0.000 1.000
#&gt; SRR1927049     2   0.000      0.924 0.000 1.000 0.000 0.000
#&gt; SRR1927047     2   0.000      0.924 0.000 1.000 0.000 0.000
#&gt; SRR1927046     1   0.000      0.986 1.000 0.000 0.000 0.000
#&gt; SRR1927045     2   0.000      0.924 0.000 1.000 0.000 0.000
#&gt; SRR1927044     1   0.130      0.953 0.956 0.000 0.000 0.044
#&gt; SRR1927043     2   0.500     -0.220 0.000 0.508 0.492 0.000
#&gt; SRR1927042     1   0.000      0.986 1.000 0.000 0.000 0.000
#&gt; SRR1927040     1   0.000      0.986 1.000 0.000 0.000 0.000
#&gt; SRR1927039     2   0.000      0.924 0.000 1.000 0.000 0.000
#&gt; SRR1927038     1   0.000      0.986 1.000 0.000 0.000 0.000
#&gt; SRR1927037     2   0.000      0.924 0.000 1.000 0.000 0.000
#&gt; SRR1927036     1   0.130      0.953 0.956 0.000 0.000 0.044
#&gt; SRR1927035     2   0.000      0.924 0.000 1.000 0.000 0.000
#&gt; SRR1927034     4   0.000      0.970 0.000 0.000 0.000 1.000
#&gt; SRR1927033     3   0.000      0.784 0.000 0.000 1.000 0.000
#&gt; SRR1927032     1   0.000      0.986 1.000 0.000 0.000 0.000
#&gt; SRR1927031     2   0.000      0.924 0.000 1.000 0.000 0.000
#&gt; SRR1927030     1   0.130      0.953 0.956 0.000 0.000 0.044
#&gt; SRR1927028     4   0.000      0.970 0.000 0.000 0.000 1.000
#&gt; SRR1927029     3   0.499      0.137 0.000 0.468 0.532 0.000
#&gt; SRR1927027     4   0.000      0.970 0.000 0.000 0.000 1.000
#&gt; SRR1927026     4   0.000      0.970 0.000 0.000 0.000 1.000
#&gt; SRR1927024     4   0.000      0.970 0.000 0.000 0.000 1.000
#&gt; SRR1927025     2   0.500     -0.213 0.000 0.512 0.488 0.000
#&gt; SRR1927023     3   0.287      0.763 0.000 0.136 0.864 0.000
#&gt; SRR1927022     4   0.000      0.970 0.000 0.000 0.000 1.000
#&gt; SRR1927021     2   0.000      0.924 0.000 1.000 0.000 0.000
#&gt; SRR1927020     4   0.000      0.970 0.000 0.000 0.000 1.000
#&gt; SRR1927019     2   0.000      0.924 0.000 1.000 0.000 0.000
#&gt; SRR1927071     4   0.000      0.970 0.000 0.000 0.000 1.000
#&gt; SRR1927069     2   0.000      0.924 0.000 1.000 0.000 0.000
#&gt; SRR1927070     4   0.466      0.452 0.348 0.000 0.000 0.652
#&gt; SRR1927068     4   0.000      0.970 0.000 0.000 0.000 1.000
#&gt; SRR1927066     4   0.000      0.970 0.000 0.000 0.000 1.000
#&gt; SRR1927065     2   0.164      0.868 0.000 0.940 0.060 0.000
#&gt; SRR1927067     3   0.312      0.752 0.000 0.156 0.844 0.000
#&gt; SRR1927064     1   0.000      0.986 1.000 0.000 0.000 0.000
#&gt; SRR1927063     2   0.000      0.924 0.000 1.000 0.000 0.000
#&gt; SRR1927062     4   0.000      0.970 0.000 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-3-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-4'>
<p><a id='tab-ATC-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1927048     1  0.0000      0.981 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927061     2  0.3177      0.713 0.000 0.792 0.208 0.000 0.000
#&gt; SRR1927060     1  0.0000      0.981 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927058     1  0.0955      0.966 0.968 0.000 0.000 0.004 0.028
#&gt; SRR1927057     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927055     3  0.0000      0.774 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927056     4  0.0000      0.964 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927054     1  0.0000      0.981 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927052     4  0.0000      0.964 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927053     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927051     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927050     4  0.0000      0.964 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927049     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927047     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927046     1  0.0000      0.981 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927045     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927044     1  0.1668      0.947 0.940 0.000 0.000 0.032 0.028
#&gt; SRR1927043     3  0.3210      0.744 0.000 0.212 0.788 0.000 0.000
#&gt; SRR1927042     1  0.0000      0.981 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      0.981 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927039     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927038     1  0.0000      0.981 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927036     1  0.1668      0.947 0.940 0.000 0.000 0.032 0.028
#&gt; SRR1927035     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927034     4  0.0000      0.964 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927033     3  0.0000      0.774 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927032     1  0.0000      0.981 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927031     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927030     1  0.1668      0.947 0.940 0.000 0.000 0.032 0.028
#&gt; SRR1927028     4  0.0000      0.964 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927029     3  0.2648      0.818 0.000 0.152 0.848 0.000 0.000
#&gt; SRR1927027     4  0.0000      0.964 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927026     4  0.0000      0.964 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927024     4  0.0000      0.964 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927025     5  0.0992      0.957 0.000 0.024 0.008 0.000 0.968
#&gt; SRR1927023     5  0.0794      0.957 0.000 0.000 0.028 0.000 0.972
#&gt; SRR1927022     4  0.0404      0.954 0.000 0.000 0.000 0.988 0.012
#&gt; SRR1927021     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927020     4  0.0000      0.964 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927019     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927071     4  0.0000      0.964 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927069     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927070     4  0.4747      0.385 0.352 0.000 0.000 0.620 0.028
#&gt; SRR1927068     4  0.0000      0.964 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927066     4  0.0000      0.964 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927065     2  0.3039      0.739 0.000 0.808 0.192 0.000 0.000
#&gt; SRR1927067     3  0.2230      0.832 0.000 0.116 0.884 0.000 0.000
#&gt; SRR1927064     1  0.0000      0.981 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927063     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1927062     4  0.0000      0.964 0.000 0.000 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-4-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-5'>
<p><a id='tab-ATC-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1927048     1  0.0000      0.943 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927061     3  0.2260      0.694 0.000 0.140 0.860 0.000 0.000 0.000
#&gt; SRR1927060     1  0.0000      0.943 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927058     1  0.2566      0.881 0.868 0.000 0.012 0.008 0.000 0.112
#&gt; SRR1927057     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927055     6  0.2562      0.923 0.000 0.000 0.172 0.000 0.000 0.828
#&gt; SRR1927056     4  0.0146      0.954 0.000 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1927054     1  0.0146      0.942 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; SRR1927052     4  0.0000      0.954 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927053     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927051     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927050     4  0.0146      0.954 0.000 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1927049     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927047     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927046     1  0.0000      0.943 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927045     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927044     1  0.3413      0.852 0.824 0.000 0.012 0.052 0.000 0.112
#&gt; SRR1927043     3  0.0713      0.745 0.000 0.028 0.972 0.000 0.000 0.000
#&gt; SRR1927042     1  0.0260      0.941 0.992 0.000 0.000 0.000 0.000 0.008
#&gt; SRR1927040     1  0.0000      0.943 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927039     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927038     1  0.0000      0.943 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927036     1  0.3413      0.852 0.824 0.000 0.012 0.052 0.000 0.112
#&gt; SRR1927035     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927034     4  0.0146      0.954 0.000 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1927033     6  0.2996      0.924 0.000 0.000 0.228 0.000 0.000 0.772
#&gt; SRR1927032     1  0.0000      0.943 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927031     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927030     1  0.3413      0.852 0.824 0.000 0.012 0.052 0.000 0.112
#&gt; SRR1927028     4  0.0000      0.954 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927029     3  0.0632      0.743 0.000 0.024 0.976 0.000 0.000 0.000
#&gt; SRR1927027     4  0.2191      0.850 0.000 0.000 0.004 0.876 0.000 0.120
#&gt; SRR1927026     4  0.0146      0.954 0.000 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1927024     4  0.0000      0.954 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927025     5  0.0363      0.975 0.000 0.012 0.000 0.000 0.988 0.000
#&gt; SRR1927023     5  0.0000      0.975 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927022     4  0.1010      0.923 0.000 0.000 0.004 0.960 0.000 0.036
#&gt; SRR1927021     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927020     4  0.0146      0.954 0.000 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1927019     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927071     4  0.0000      0.954 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927069     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927070     4  0.5285      0.416 0.260 0.000 0.012 0.616 0.000 0.112
#&gt; SRR1927068     4  0.0146      0.954 0.000 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1927066     4  0.0000      0.954 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927065     3  0.3659      0.419 0.000 0.364 0.636 0.000 0.000 0.000
#&gt; SRR1927067     3  0.0458      0.730 0.000 0.016 0.984 0.000 0.000 0.000
#&gt; SRR1927064     1  0.0000      0.943 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927063     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927062     4  0.0000      0.954 0.000 0.000 0.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-5-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-signatures'>
<ul>
<li><a href='#tab-ATC-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-skmeans-signature_compare](figure_cola/ATC-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-skmeans-collect-classes](figure_cola/ATC-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:pam**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "pam"]
# you can also extract it by
# res = res_list["ATC:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16868 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-pam-collect-plots](figure_cola/ATC-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-pam-select-partition-number](figure_cola/ATC-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.4982 0.502   0.502
#> 3 3 0.978           0.966       0.984         0.3277 0.837   0.676
#> 4 4 1.000           0.979       0.991         0.1390 0.886   0.675
#> 5 5 0.984           0.950       0.977         0.0555 0.928   0.727
#> 6 6 0.984           0.938       0.973         0.0121 0.989   0.949
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2 3 4 5
```

There is also optional best $k$ = 2 3 4 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-classes'>
<ul>
<li><a href='#tab-ATC-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-pam-get-classes-1'>
<p><a id='tab-ATC-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1927048     1       0          1  1  0
#&gt; SRR1927061     2       0          1  0  1
#&gt; SRR1927060     1       0          1  1  0
#&gt; SRR1927059     2       0          1  0  1
#&gt; SRR1927058     1       0          1  1  0
#&gt; SRR1927057     2       0          1  0  1
#&gt; SRR1927055     1       0          1  1  0
#&gt; SRR1927056     1       0          1  1  0
#&gt; SRR1927054     1       0          1  1  0
#&gt; SRR1927052     1       0          1  1  0
#&gt; SRR1927053     2       0          1  0  1
#&gt; SRR1927051     2       0          1  0  1
#&gt; SRR1927050     1       0          1  1  0
#&gt; SRR1927049     2       0          1  0  1
#&gt; SRR1927047     2       0          1  0  1
#&gt; SRR1927046     1       0          1  1  0
#&gt; SRR1927045     2       0          1  0  1
#&gt; SRR1927044     1       0          1  1  0
#&gt; SRR1927043     2       0          1  0  1
#&gt; SRR1927042     1       0          1  1  0
#&gt; SRR1927040     1       0          1  1  0
#&gt; SRR1927039     2       0          1  0  1
#&gt; SRR1927038     1       0          1  1  0
#&gt; SRR1927037     2       0          1  0  1
#&gt; SRR1927036     1       0          1  1  0
#&gt; SRR1927035     2       0          1  0  1
#&gt; SRR1927034     1       0          1  1  0
#&gt; SRR1927033     2       0          1  0  1
#&gt; SRR1927032     1       0          1  1  0
#&gt; SRR1927031     2       0          1  0  1
#&gt; SRR1927030     1       0          1  1  0
#&gt; SRR1927028     1       0          1  1  0
#&gt; SRR1927029     2       0          1  0  1
#&gt; SRR1927027     1       0          1  1  0
#&gt; SRR1927026     1       0          1  1  0
#&gt; SRR1927024     1       0          1  1  0
#&gt; SRR1927025     2       0          1  0  1
#&gt; SRR1927023     1       0          1  1  0
#&gt; SRR1927022     1       0          1  1  0
#&gt; SRR1927021     2       0          1  0  1
#&gt; SRR1927020     1       0          1  1  0
#&gt; SRR1927019     2       0          1  0  1
#&gt; SRR1927071     1       0          1  1  0
#&gt; SRR1927069     2       0          1  0  1
#&gt; SRR1927070     1       0          1  1  0
#&gt; SRR1927068     1       0          1  1  0
#&gt; SRR1927066     1       0          1  1  0
#&gt; SRR1927065     2       0          1  0  1
#&gt; SRR1927067     2       0          1  0  1
#&gt; SRR1927064     1       0          1  1  0
#&gt; SRR1927063     2       0          1  0  1
#&gt; SRR1927062     1       0          1  1  0
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-1-a').click(function(){
  $('#tab-ATC-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-2'>
<p><a id='tab-ATC-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1 p2    p3
#&gt; SRR1927048     1   0.000      0.960 1.000  0 0.000
#&gt; SRR1927061     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1927060     1   0.000      0.960 1.000  0 0.000
#&gt; SRR1927059     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1927058     1   0.000      0.960 1.000  0 0.000
#&gt; SRR1927057     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1927055     1   0.455      0.769 0.800  0 0.200
#&gt; SRR1927056     3   0.000      0.983 0.000  0 1.000
#&gt; SRR1927054     1   0.000      0.960 1.000  0 0.000
#&gt; SRR1927052     1   0.480      0.743 0.780  0 0.220
#&gt; SRR1927053     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1927051     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1927050     3   0.000      0.983 0.000  0 1.000
#&gt; SRR1927049     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1927047     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1927046     1   0.000      0.960 1.000  0 0.000
#&gt; SRR1927045     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1927044     1   0.000      0.960 1.000  0 0.000
#&gt; SRR1927043     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1927042     1   0.000      0.960 1.000  0 0.000
#&gt; SRR1927040     1   0.000      0.960 1.000  0 0.000
#&gt; SRR1927039     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1927038     1   0.000      0.960 1.000  0 0.000
#&gt; SRR1927037     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1927036     1   0.000      0.960 1.000  0 0.000
#&gt; SRR1927035     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1927034     3   0.000      0.983 0.000  0 1.000
#&gt; SRR1927033     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1927032     1   0.000      0.960 1.000  0 0.000
#&gt; SRR1927031     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1927030     1   0.000      0.960 1.000  0 0.000
#&gt; SRR1927028     3   0.000      0.983 0.000  0 1.000
#&gt; SRR1927029     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1927027     3   0.424      0.769 0.176  0 0.824
#&gt; SRR1927026     3   0.000      0.983 0.000  0 1.000
#&gt; SRR1927024     3   0.000      0.983 0.000  0 1.000
#&gt; SRR1927025     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1927023     1   0.000      0.960 1.000  0 0.000
#&gt; SRR1927022     1   0.480      0.743 0.780  0 0.220
#&gt; SRR1927021     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1927020     3   0.000      0.983 0.000  0 1.000
#&gt; SRR1927019     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1927071     3   0.000      0.983 0.000  0 1.000
#&gt; SRR1927069     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1927070     1   0.000      0.960 1.000  0 0.000
#&gt; SRR1927068     3   0.000      0.983 0.000  0 1.000
#&gt; SRR1927066     3   0.000      0.983 0.000  0 1.000
#&gt; SRR1927065     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1927067     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1927064     1   0.000      0.960 1.000  0 0.000
#&gt; SRR1927063     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1927062     3   0.000      0.983 0.000  0 1.000
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-2-a').click(function(){
  $('#tab-ATC-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-3'>
<p><a id='tab-ATC-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1 p2 p3    p4
#&gt; SRR1927048     1   0.000      0.978 1.000  0  0 0.000
#&gt; SRR1927061     3   0.000      1.000 0.000  0  1 0.000
#&gt; SRR1927060     1   0.000      0.978 1.000  0  0 0.000
#&gt; SRR1927059     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1927058     1   0.000      0.978 1.000  0  0 0.000
#&gt; SRR1927057     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1927055     3   0.000      1.000 0.000  0  1 0.000
#&gt; SRR1927056     4   0.000      0.981 0.000  0  0 1.000
#&gt; SRR1927054     1   0.000      0.978 1.000  0  0 0.000
#&gt; SRR1927052     1   0.312      0.822 0.844  0  0 0.156
#&gt; SRR1927053     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1927051     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1927050     4   0.000      0.981 0.000  0  0 1.000
#&gt; SRR1927049     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1927047     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1927046     1   0.000      0.978 1.000  0  0 0.000
#&gt; SRR1927045     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1927044     1   0.000      0.978 1.000  0  0 0.000
#&gt; SRR1927043     3   0.000      1.000 0.000  0  1 0.000
#&gt; SRR1927042     1   0.000      0.978 1.000  0  0 0.000
#&gt; SRR1927040     1   0.000      0.978 1.000  0  0 0.000
#&gt; SRR1927039     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1927038     1   0.000      0.978 1.000  0  0 0.000
#&gt; SRR1927037     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1927036     1   0.000      0.978 1.000  0  0 0.000
#&gt; SRR1927035     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1927034     4   0.000      0.981 0.000  0  0 1.000
#&gt; SRR1927033     3   0.000      1.000 0.000  0  1 0.000
#&gt; SRR1927032     1   0.000      0.978 1.000  0  0 0.000
#&gt; SRR1927031     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1927030     1   0.000      0.978 1.000  0  0 0.000
#&gt; SRR1927028     4   0.000      0.981 0.000  0  0 1.000
#&gt; SRR1927029     3   0.000      1.000 0.000  0  1 0.000
#&gt; SRR1927027     4   0.336      0.777 0.176  0  0 0.824
#&gt; SRR1927026     4   0.000      0.981 0.000  0  0 1.000
#&gt; SRR1927024     4   0.000      0.981 0.000  0  0 1.000
#&gt; SRR1927025     3   0.000      1.000 0.000  0  1 0.000
#&gt; SRR1927023     3   0.000      1.000 0.000  0  1 0.000
#&gt; SRR1927022     1   0.312      0.822 0.844  0  0 0.156
#&gt; SRR1927021     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1927020     4   0.000      0.981 0.000  0  0 1.000
#&gt; SRR1927019     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1927071     4   0.000      0.981 0.000  0  0 1.000
#&gt; SRR1927069     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1927070     1   0.000      0.978 1.000  0  0 0.000
#&gt; SRR1927068     4   0.000      0.981 0.000  0  0 1.000
#&gt; SRR1927066     4   0.000      0.981 0.000  0  0 1.000
#&gt; SRR1927065     3   0.000      1.000 0.000  0  1 0.000
#&gt; SRR1927067     3   0.000      1.000 0.000  0  1 0.000
#&gt; SRR1927064     1   0.000      0.978 1.000  0  0 0.000
#&gt; SRR1927063     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1927062     4   0.000      0.981 0.000  0  0 1.000
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-3-a').click(function(){
  $('#tab-ATC-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-4'>
<p><a id='tab-ATC-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette   p1 p2 p3    p4    p5
#&gt; SRR1927048     1   0.000      1.000 1.00  0  0 0.000 0.000
#&gt; SRR1927061     3   0.000      1.000 0.00  0  1 0.000 0.000
#&gt; SRR1927060     1   0.000      1.000 1.00  0  0 0.000 0.000
#&gt; SRR1927059     2   0.000      1.000 0.00  1  0 0.000 0.000
#&gt; SRR1927058     1   0.000      1.000 1.00  0  0 0.000 0.000
#&gt; SRR1927057     2   0.000      1.000 0.00  1  0 0.000 0.000
#&gt; SRR1927055     3   0.000      1.000 0.00  0  1 0.000 0.000
#&gt; SRR1927056     5   0.000      1.000 0.00  0  0 0.000 1.000
#&gt; SRR1927054     1   0.000      1.000 1.00  0  0 0.000 0.000
#&gt; SRR1927052     4   0.000      0.856 0.00  0  0 1.000 0.000
#&gt; SRR1927053     2   0.000      1.000 0.00  1  0 0.000 0.000
#&gt; SRR1927051     2   0.000      1.000 0.00  1  0 0.000 0.000
#&gt; SRR1927050     5   0.000      1.000 0.00  0  0 0.000 1.000
#&gt; SRR1927049     2   0.000      1.000 0.00  1  0 0.000 0.000
#&gt; SRR1927047     2   0.000      1.000 0.00  1  0 0.000 0.000
#&gt; SRR1927046     1   0.000      1.000 1.00  0  0 0.000 0.000
#&gt; SRR1927045     2   0.000      1.000 0.00  1  0 0.000 0.000
#&gt; SRR1927044     1   0.000      1.000 1.00  0  0 0.000 0.000
#&gt; SRR1927043     3   0.000      1.000 0.00  0  1 0.000 0.000
#&gt; SRR1927042     1   0.000      1.000 1.00  0  0 0.000 0.000
#&gt; SRR1927040     1   0.000      1.000 1.00  0  0 0.000 0.000
#&gt; SRR1927039     2   0.000      1.000 0.00  1  0 0.000 0.000
#&gt; SRR1927038     1   0.000      1.000 1.00  0  0 0.000 0.000
#&gt; SRR1927037     2   0.000      1.000 0.00  1  0 0.000 0.000
#&gt; SRR1927036     1   0.000      1.000 1.00  0  0 0.000 0.000
#&gt; SRR1927035     2   0.000      1.000 0.00  1  0 0.000 0.000
#&gt; SRR1927034     5   0.000      1.000 0.00  0  0 0.000 1.000
#&gt; SRR1927033     3   0.000      1.000 0.00  0  1 0.000 0.000
#&gt; SRR1927032     1   0.000      1.000 1.00  0  0 0.000 0.000
#&gt; SRR1927031     2   0.000      1.000 0.00  1  0 0.000 0.000
#&gt; SRR1927030     1   0.000      1.000 1.00  0  0 0.000 0.000
#&gt; SRR1927028     4   0.000      0.856 0.00  0  0 1.000 0.000
#&gt; SRR1927029     3   0.000      1.000 0.00  0  1 0.000 0.000
#&gt; SRR1927027     4   0.418      0.388 0.00  0  0 0.600 0.400
#&gt; SRR1927026     4   0.413      0.476 0.00  0  0 0.620 0.380
#&gt; SRR1927024     4   0.000      0.856 0.00  0  0 1.000 0.000
#&gt; SRR1927025     3   0.000      1.000 0.00  0  1 0.000 0.000
#&gt; SRR1927023     3   0.000      1.000 0.00  0  1 0.000 0.000
#&gt; SRR1927022     4   0.000      0.856 0.00  0  0 1.000 0.000
#&gt; SRR1927021     2   0.000      1.000 0.00  1  0 0.000 0.000
#&gt; SRR1927020     5   0.000      1.000 0.00  0  0 0.000 1.000
#&gt; SRR1927019     2   0.000      1.000 0.00  1  0 0.000 0.000
#&gt; SRR1927071     4   0.000      0.856 0.00  0  0 1.000 0.000
#&gt; SRR1927069     2   0.000      1.000 0.00  1  0 0.000 0.000
#&gt; SRR1927070     4   0.293      0.701 0.18  0  0 0.820 0.000
#&gt; SRR1927068     5   0.000      1.000 0.00  0  0 0.000 1.000
#&gt; SRR1927066     4   0.000      0.856 0.00  0  0 1.000 0.000
#&gt; SRR1927065     3   0.000      1.000 0.00  0  1 0.000 0.000
#&gt; SRR1927067     3   0.000      1.000 0.00  0  1 0.000 0.000
#&gt; SRR1927064     1   0.000      1.000 1.00  0  0 0.000 0.000
#&gt; SRR1927063     2   0.000      1.000 0.00  1  0 0.000 0.000
#&gt; SRR1927062     4   0.331      0.685 0.00  0  0 0.776 0.224
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-4-a').click(function(){
  $('#tab-ATC-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-5'>
<p><a id='tab-ATC-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette   p1 p2    p3    p4    p5    p6
#&gt; SRR1927048     1   0.000      1.000 1.00  0 0.000 0.000 0.000 0.000
#&gt; SRR1927061     3   0.000      1.000 0.00  0 1.000 0.000 0.000 0.000
#&gt; SRR1927060     1   0.000      1.000 1.00  0 0.000 0.000 0.000 0.000
#&gt; SRR1927059     2   0.000      1.000 0.00  1 0.000 0.000 0.000 0.000
#&gt; SRR1927058     1   0.000      1.000 1.00  0 0.000 0.000 0.000 0.000
#&gt; SRR1927057     2   0.000      1.000 0.00  1 0.000 0.000 0.000 0.000
#&gt; SRR1927055     3   0.000      1.000 0.00  0 1.000 0.000 0.000 0.000
#&gt; SRR1927056     6   0.000      1.000 0.00  0 0.000 0.000 0.000 1.000
#&gt; SRR1927054     1   0.000      1.000 1.00  0 0.000 0.000 0.000 0.000
#&gt; SRR1927052     4   0.000      0.842 0.00  0 0.000 1.000 0.000 0.000
#&gt; SRR1927053     2   0.000      1.000 0.00  1 0.000 0.000 0.000 0.000
#&gt; SRR1927051     2   0.000      1.000 0.00  1 0.000 0.000 0.000 0.000
#&gt; SRR1927050     6   0.000      1.000 0.00  0 0.000 0.000 0.000 1.000
#&gt; SRR1927049     2   0.000      1.000 0.00  1 0.000 0.000 0.000 0.000
#&gt; SRR1927047     2   0.000      1.000 0.00  1 0.000 0.000 0.000 0.000
#&gt; SRR1927046     1   0.000      1.000 1.00  0 0.000 0.000 0.000 0.000
#&gt; SRR1927045     2   0.000      1.000 0.00  1 0.000 0.000 0.000 0.000
#&gt; SRR1927044     1   0.000      1.000 1.00  0 0.000 0.000 0.000 0.000
#&gt; SRR1927043     3   0.000      1.000 0.00  0 1.000 0.000 0.000 0.000
#&gt; SRR1927042     1   0.000      1.000 1.00  0 0.000 0.000 0.000 0.000
#&gt; SRR1927040     1   0.000      1.000 1.00  0 0.000 0.000 0.000 0.000
#&gt; SRR1927039     2   0.000      1.000 0.00  1 0.000 0.000 0.000 0.000
#&gt; SRR1927038     1   0.000      1.000 1.00  0 0.000 0.000 0.000 0.000
#&gt; SRR1927037     2   0.000      1.000 0.00  1 0.000 0.000 0.000 0.000
#&gt; SRR1927036     1   0.000      1.000 1.00  0 0.000 0.000 0.000 0.000
#&gt; SRR1927035     2   0.000      1.000 0.00  1 0.000 0.000 0.000 0.000
#&gt; SRR1927034     6   0.000      1.000 0.00  0 0.000 0.000 0.000 1.000
#&gt; SRR1927033     3   0.000      1.000 0.00  0 1.000 0.000 0.000 0.000
#&gt; SRR1927032     1   0.000      1.000 1.00  0 0.000 0.000 0.000 0.000
#&gt; SRR1927031     2   0.000      1.000 0.00  1 0.000 0.000 0.000 0.000
#&gt; SRR1927030     1   0.000      1.000 1.00  0 0.000 0.000 0.000 0.000
#&gt; SRR1927028     4   0.000      0.842 0.00  0 0.000 1.000 0.000 0.000
#&gt; SRR1927029     3   0.000      1.000 0.00  0 1.000 0.000 0.000 0.000
#&gt; SRR1927027     4   0.376      0.389 0.00  0 0.000 0.600 0.000 0.400
#&gt; SRR1927026     4   0.370      0.485 0.00  0 0.000 0.624 0.000 0.376
#&gt; SRR1927024     4   0.000      0.842 0.00  0 0.000 1.000 0.000 0.000
#&gt; SRR1927025     5   0.285      0.737 0.00  0 0.208 0.000 0.792 0.000
#&gt; SRR1927023     5   0.000      0.764 0.00  0 0.000 0.000 1.000 0.000
#&gt; SRR1927022     4   0.000      0.842 0.00  0 0.000 1.000 0.000 0.000
#&gt; SRR1927021     2   0.000      1.000 0.00  1 0.000 0.000 0.000 0.000
#&gt; SRR1927020     6   0.000      1.000 0.00  0 0.000 0.000 0.000 1.000
#&gt; SRR1927019     2   0.000      1.000 0.00  1 0.000 0.000 0.000 0.000
#&gt; SRR1927071     4   0.000      0.842 0.00  0 0.000 1.000 0.000 0.000
#&gt; SRR1927069     2   0.000      1.000 0.00  1 0.000 0.000 0.000 0.000
#&gt; SRR1927070     4   0.263      0.661 0.18  0 0.000 0.820 0.000 0.000
#&gt; SRR1927068     6   0.000      1.000 0.00  0 0.000 0.000 0.000 1.000
#&gt; SRR1927066     4   0.000      0.842 0.00  0 0.000 1.000 0.000 0.000
#&gt; SRR1927065     3   0.000      1.000 0.00  0 1.000 0.000 0.000 0.000
#&gt; SRR1927067     3   0.000      1.000 0.00  0 1.000 0.000 0.000 0.000
#&gt; SRR1927064     1   0.000      1.000 1.00  0 0.000 0.000 0.000 0.000
#&gt; SRR1927063     2   0.000      1.000 0.00  1 0.000 0.000 0.000 0.000
#&gt; SRR1927062     4   0.294      0.691 0.00  0 0.000 0.780 0.000 0.220
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-5-a').click(function(){
  $('#tab-ATC-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-signatures'>
<ul>
<li><a href='#tab-ATC-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-1-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-1"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-2-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-2"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-3-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-3"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-4-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-4"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-5-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-pam-signature_compare](figure_cola/ATC-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-pam-collect-classes](figure_cola/ATC-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:mclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "mclust"]
# you can also extract it by
# res = res_list["ATC:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16868 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-mclust-collect-plots](figure_cola/ATC-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-mclust-select-partition-number](figure_cola/ATC-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5095 0.491   0.491
#> 3 3 0.889           0.975       0.972         0.1909 0.897   0.791
#> 4 4 0.885           0.871       0.937         0.1892 0.754   0.476
#> 5 5 1.000           0.997       0.999         0.0741 0.921   0.739
#> 6 6 1.000           0.971       0.989         0.0542 0.958   0.812
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2 5
```

There is also optional best $k$ = 2 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-classes'>
<ul>
<li><a href='#tab-ATC-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-mclust-get-classes-1'>
<p><a id='tab-ATC-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1927048     1       0          1  1  0
#&gt; SRR1927061     2       0          1  0  1
#&gt; SRR1927060     1       0          1  1  0
#&gt; SRR1927059     2       0          1  0  1
#&gt; SRR1927058     1       0          1  1  0
#&gt; SRR1927057     2       0          1  0  1
#&gt; SRR1927055     2       0          1  0  1
#&gt; SRR1927056     1       0          1  1  0
#&gt; SRR1927054     1       0          1  1  0
#&gt; SRR1927052     1       0          1  1  0
#&gt; SRR1927053     2       0          1  0  1
#&gt; SRR1927051     2       0          1  0  1
#&gt; SRR1927050     1       0          1  1  0
#&gt; SRR1927049     2       0          1  0  1
#&gt; SRR1927047     2       0          1  0  1
#&gt; SRR1927046     1       0          1  1  0
#&gt; SRR1927045     2       0          1  0  1
#&gt; SRR1927044     1       0          1  1  0
#&gt; SRR1927043     2       0          1  0  1
#&gt; SRR1927042     1       0          1  1  0
#&gt; SRR1927040     1       0          1  1  0
#&gt; SRR1927039     2       0          1  0  1
#&gt; SRR1927038     1       0          1  1  0
#&gt; SRR1927037     2       0          1  0  1
#&gt; SRR1927036     1       0          1  1  0
#&gt; SRR1927035     2       0          1  0  1
#&gt; SRR1927034     1       0          1  1  0
#&gt; SRR1927033     2       0          1  0  1
#&gt; SRR1927032     1       0          1  1  0
#&gt; SRR1927031     2       0          1  0  1
#&gt; SRR1927030     1       0          1  1  0
#&gt; SRR1927028     1       0          1  1  0
#&gt; SRR1927029     2       0          1  0  1
#&gt; SRR1927027     2       0          1  0  1
#&gt; SRR1927026     1       0          1  1  0
#&gt; SRR1927024     1       0          1  1  0
#&gt; SRR1927025     2       0          1  0  1
#&gt; SRR1927023     2       0          1  0  1
#&gt; SRR1927022     1       0          1  1  0
#&gt; SRR1927021     2       0          1  0  1
#&gt; SRR1927020     1       0          1  1  0
#&gt; SRR1927019     2       0          1  0  1
#&gt; SRR1927071     1       0          1  1  0
#&gt; SRR1927069     2       0          1  0  1
#&gt; SRR1927070     1       0          1  1  0
#&gt; SRR1927068     1       0          1  1  0
#&gt; SRR1927066     1       0          1  1  0
#&gt; SRR1927065     2       0          1  0  1
#&gt; SRR1927067     2       0          1  0  1
#&gt; SRR1927064     1       0          1  1  0
#&gt; SRR1927063     2       0          1  0  1
#&gt; SRR1927062     1       0          1  1  0
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-1-a').click(function(){
  $('#tab-ATC-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-2'>
<p><a id='tab-ATC-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1927048     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1927061     3   0.375      0.975 0.000 0.144 0.856
#&gt; SRR1927060     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1927059     2   0.000      0.976 0.000 1.000 0.000
#&gt; SRR1927058     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1927057     2   0.000      0.976 0.000 1.000 0.000
#&gt; SRR1927055     3   0.375      0.975 0.000 0.144 0.856
#&gt; SRR1927056     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1927054     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1927052     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1927053     2   0.000      0.976 0.000 1.000 0.000
#&gt; SRR1927051     2   0.000      0.976 0.000 1.000 0.000
#&gt; SRR1927050     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1927049     2   0.000      0.976 0.000 1.000 0.000
#&gt; SRR1927047     2   0.000      0.976 0.000 1.000 0.000
#&gt; SRR1927046     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1927045     2   0.000      0.976 0.000 1.000 0.000
#&gt; SRR1927044     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1927043     3   0.375      0.975 0.000 0.144 0.856
#&gt; SRR1927042     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1927040     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1927039     2   0.000      0.976 0.000 1.000 0.000
#&gt; SRR1927038     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1927037     2   0.000      0.976 0.000 1.000 0.000
#&gt; SRR1927036     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1927035     2   0.000      0.976 0.000 1.000 0.000
#&gt; SRR1927034     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1927033     3   0.375      0.975 0.000 0.144 0.856
#&gt; SRR1927032     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1927031     2   0.000      0.976 0.000 1.000 0.000
#&gt; SRR1927030     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1927028     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1927029     3   0.375      0.975 0.000 0.144 0.856
#&gt; SRR1927027     3   0.000      0.837 0.000 0.000 1.000
#&gt; SRR1927026     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1927024     1   0.327      0.882 0.884 0.000 0.116
#&gt; SRR1927025     2   0.424      0.810 0.000 0.824 0.176
#&gt; SRR1927023     2   0.424      0.810 0.000 0.824 0.176
#&gt; SRR1927022     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1927021     2   0.000      0.976 0.000 1.000 0.000
#&gt; SRR1927020     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1927019     2   0.000      0.976 0.000 1.000 0.000
#&gt; SRR1927071     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1927069     2   0.000      0.976 0.000 1.000 0.000
#&gt; SRR1927070     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1927068     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1927066     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1927065     3   0.375      0.975 0.000 0.144 0.856
#&gt; SRR1927067     3   0.375      0.975 0.000 0.144 0.856
#&gt; SRR1927064     1   0.000      0.996 1.000 0.000 0.000
#&gt; SRR1927063     2   0.000      0.976 0.000 1.000 0.000
#&gt; SRR1927062     1   0.000      0.996 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-2-a').click(function(){
  $('#tab-ATC-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-3'>
<p><a id='tab-ATC-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1927048     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1927061     2  0.0000      0.491 0.000 1.000 0.000 0.000
#&gt; SRR1927060     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.4898      0.837 0.000 0.584 0.416 0.000
#&gt; SRR1927058     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1927057     2  0.4898      0.837 0.000 0.584 0.416 0.000
#&gt; SRR1927055     2  0.0000      0.491 0.000 1.000 0.000 0.000
#&gt; SRR1927056     4  0.0921      0.962 0.028 0.000 0.000 0.972
#&gt; SRR1927054     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1927052     4  0.0921      0.962 0.028 0.000 0.000 0.972
#&gt; SRR1927053     2  0.4898      0.837 0.000 0.584 0.416 0.000
#&gt; SRR1927051     2  0.4898      0.837 0.000 0.584 0.416 0.000
#&gt; SRR1927050     4  0.0000      0.966 0.000 0.000 0.000 1.000
#&gt; SRR1927049     2  0.4898      0.837 0.000 0.584 0.416 0.000
#&gt; SRR1927047     2  0.4898      0.837 0.000 0.584 0.416 0.000
#&gt; SRR1927046     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1927045     2  0.4898      0.837 0.000 0.584 0.416 0.000
#&gt; SRR1927044     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1927043     2  0.0000      0.491 0.000 1.000 0.000 0.000
#&gt; SRR1927042     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1927039     2  0.4898      0.837 0.000 0.584 0.416 0.000
#&gt; SRR1927038     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.4898      0.837 0.000 0.584 0.416 0.000
#&gt; SRR1927036     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1927035     2  0.4898      0.837 0.000 0.584 0.416 0.000
#&gt; SRR1927034     4  0.0000      0.966 0.000 0.000 0.000 1.000
#&gt; SRR1927033     2  0.0000      0.491 0.000 1.000 0.000 0.000
#&gt; SRR1927032     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1927031     2  0.4898      0.837 0.000 0.584 0.416 0.000
#&gt; SRR1927030     1  0.0188      0.995 0.996 0.000 0.000 0.004
#&gt; SRR1927028     4  0.0921      0.962 0.028 0.000 0.000 0.972
#&gt; SRR1927029     2  0.0000      0.491 0.000 1.000 0.000 0.000
#&gt; SRR1927027     3  0.4898      1.000 0.000 0.416 0.584 0.000
#&gt; SRR1927026     4  0.0000      0.966 0.000 0.000 0.000 1.000
#&gt; SRR1927024     4  0.0000      0.966 0.000 0.000 0.000 1.000
#&gt; SRR1927025     3  0.4898      1.000 0.000 0.416 0.584 0.000
#&gt; SRR1927023     3  0.4898      1.000 0.000 0.416 0.584 0.000
#&gt; SRR1927022     4  0.0000      0.966 0.000 0.000 0.000 1.000
#&gt; SRR1927021     2  0.4898      0.837 0.000 0.584 0.416 0.000
#&gt; SRR1927020     4  0.0000      0.966 0.000 0.000 0.000 1.000
#&gt; SRR1927019     2  0.4898      0.837 0.000 0.584 0.416 0.000
#&gt; SRR1927071     4  0.0921      0.962 0.028 0.000 0.000 0.972
#&gt; SRR1927069     2  0.4898      0.837 0.000 0.584 0.416 0.000
#&gt; SRR1927070     1  0.0336      0.990 0.992 0.000 0.000 0.008
#&gt; SRR1927068     4  0.0000      0.966 0.000 0.000 0.000 1.000
#&gt; SRR1927066     4  0.0921      0.962 0.028 0.000 0.000 0.972
#&gt; SRR1927065     2  0.0000      0.491 0.000 1.000 0.000 0.000
#&gt; SRR1927067     2  0.0000      0.491 0.000 1.000 0.000 0.000
#&gt; SRR1927064     1  0.0000      0.999 1.000 0.000 0.000 0.000
#&gt; SRR1927063     2  0.4898      0.837 0.000 0.584 0.416 0.000
#&gt; SRR1927062     4  0.3486      0.761 0.188 0.000 0.000 0.812
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-3-a').click(function(){
  $('#tab-ATC-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-4'>
<p><a id='tab-ATC-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1   p2   p3 p4 p5
#&gt; SRR1927048     1   0.000      1.000  1 0.00 0.00  0  0
#&gt; SRR1927061     3   0.000      0.985  0 0.00 1.00  0  0
#&gt; SRR1927060     1   0.000      1.000  1 0.00 0.00  0  0
#&gt; SRR1927059     2   0.000      1.000  0 1.00 0.00  0  0
#&gt; SRR1927058     1   0.000      1.000  1 0.00 0.00  0  0
#&gt; SRR1927057     2   0.000      1.000  0 1.00 0.00  0  0
#&gt; SRR1927055     3   0.000      0.985  0 0.00 1.00  0  0
#&gt; SRR1927056     4   0.000      1.000  0 0.00 0.00  1  0
#&gt; SRR1927054     1   0.000      1.000  1 0.00 0.00  0  0
#&gt; SRR1927052     4   0.000      1.000  0 0.00 0.00  1  0
#&gt; SRR1927053     2   0.000      1.000  0 1.00 0.00  0  0
#&gt; SRR1927051     2   0.000      1.000  0 1.00 0.00  0  0
#&gt; SRR1927050     4   0.000      1.000  0 0.00 0.00  1  0
#&gt; SRR1927049     2   0.000      1.000  0 1.00 0.00  0  0
#&gt; SRR1927047     2   0.000      1.000  0 1.00 0.00  0  0
#&gt; SRR1927046     1   0.000      1.000  1 0.00 0.00  0  0
#&gt; SRR1927045     2   0.000      1.000  0 1.00 0.00  0  0
#&gt; SRR1927044     1   0.000      1.000  1 0.00 0.00  0  0
#&gt; SRR1927043     3   0.000      0.985  0 0.00 1.00  0  0
#&gt; SRR1927042     1   0.000      1.000  1 0.00 0.00  0  0
#&gt; SRR1927040     1   0.000      1.000  1 0.00 0.00  0  0
#&gt; SRR1927039     2   0.000      1.000  0 1.00 0.00  0  0
#&gt; SRR1927038     1   0.000      1.000  1 0.00 0.00  0  0
#&gt; SRR1927037     2   0.000      1.000  0 1.00 0.00  0  0
#&gt; SRR1927036     1   0.000      1.000  1 0.00 0.00  0  0
#&gt; SRR1927035     2   0.000      1.000  0 1.00 0.00  0  0
#&gt; SRR1927034     4   0.000      1.000  0 0.00 0.00  1  0
#&gt; SRR1927033     3   0.000      0.985  0 0.00 1.00  0  0
#&gt; SRR1927032     1   0.000      1.000  1 0.00 0.00  0  0
#&gt; SRR1927031     2   0.000      1.000  0 1.00 0.00  0  0
#&gt; SRR1927030     1   0.000      1.000  1 0.00 0.00  0  0
#&gt; SRR1927028     4   0.000      1.000  0 0.00 0.00  1  0
#&gt; SRR1927029     3   0.000      0.985  0 0.00 1.00  0  0
#&gt; SRR1927027     5   0.000      1.000  0 0.00 0.00  0  1
#&gt; SRR1927026     4   0.000      1.000  0 0.00 0.00  1  0
#&gt; SRR1927024     4   0.000      1.000  0 0.00 0.00  1  0
#&gt; SRR1927025     5   0.000      1.000  0 0.00 0.00  0  1
#&gt; SRR1927023     5   0.000      1.000  0 0.00 0.00  0  1
#&gt; SRR1927022     4   0.000      1.000  0 0.00 0.00  1  0
#&gt; SRR1927021     2   0.000      1.000  0 1.00 0.00  0  0
#&gt; SRR1927020     4   0.000      1.000  0 0.00 0.00  1  0
#&gt; SRR1927019     2   0.000      1.000  0 1.00 0.00  0  0
#&gt; SRR1927071     4   0.000      1.000  0 0.00 0.00  1  0
#&gt; SRR1927069     2   0.000      1.000  0 1.00 0.00  0  0
#&gt; SRR1927070     1   0.000      1.000  1 0.00 0.00  0  0
#&gt; SRR1927068     4   0.000      1.000  0 0.00 0.00  1  0
#&gt; SRR1927066     4   0.000      1.000  0 0.00 0.00  1  0
#&gt; SRR1927065     3   0.141      0.908  0 0.06 0.94  0  0
#&gt; SRR1927067     3   0.000      0.985  0 0.00 1.00  0  0
#&gt; SRR1927064     1   0.000      1.000  1 0.00 0.00  0  0
#&gt; SRR1927063     2   0.000      1.000  0 1.00 0.00  0  0
#&gt; SRR1927062     4   0.000      1.000  0 0.00 0.00  1  0
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-4-a').click(function(){
  $('#tab-ATC-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-5'>
<p><a id='tab-ATC-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4 p5    p6
#&gt; SRR1927048     1  0.0000      1.000 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1927061     3  0.3101      0.672 0.000 0.244 0.756 0.000  0 0.000
#&gt; SRR1927060     1  0.0000      1.000 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1927059     6  0.2823      0.724 0.000 0.204 0.000 0.000  0 0.796
#&gt; SRR1927058     1  0.0000      1.000 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1927057     2  0.2300      0.812 0.000 0.856 0.000 0.000  0 0.144
#&gt; SRR1927055     3  0.0000      0.950 0.000 0.000 1.000 0.000  0 0.000
#&gt; SRR1927056     4  0.0000      1.000 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1927054     1  0.0000      1.000 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1927052     4  0.0000      1.000 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1927053     6  0.0000      0.958 0.000 0.000 0.000 0.000  0 1.000
#&gt; SRR1927051     2  0.0000      0.975 0.000 1.000 0.000 0.000  0 0.000
#&gt; SRR1927050     4  0.0000      1.000 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1927049     2  0.0000      0.975 0.000 1.000 0.000 0.000  0 0.000
#&gt; SRR1927047     6  0.0000      0.958 0.000 0.000 0.000 0.000  0 1.000
#&gt; SRR1927046     1  0.0000      1.000 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1927045     2  0.0000      0.975 0.000 1.000 0.000 0.000  0 0.000
#&gt; SRR1927044     1  0.0000      1.000 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1927043     3  0.0000      0.950 0.000 0.000 1.000 0.000  0 0.000
#&gt; SRR1927042     1  0.0000      1.000 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1927040     1  0.0000      1.000 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1927039     6  0.0000      0.958 0.000 0.000 0.000 0.000  0 1.000
#&gt; SRR1927038     1  0.0000      1.000 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1927037     2  0.0000      0.975 0.000 1.000 0.000 0.000  0 0.000
#&gt; SRR1927036     1  0.0000      1.000 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1927035     2  0.0000      0.975 0.000 1.000 0.000 0.000  0 0.000
#&gt; SRR1927034     4  0.0000      1.000 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1927033     3  0.0000      0.950 0.000 0.000 1.000 0.000  0 0.000
#&gt; SRR1927032     1  0.0000      1.000 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1927031     6  0.0000      0.958 0.000 0.000 0.000 0.000  0 1.000
#&gt; SRR1927030     1  0.0000      1.000 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1927028     4  0.0000      1.000 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1927029     3  0.0000      0.950 0.000 0.000 1.000 0.000  0 0.000
#&gt; SRR1927027     5  0.0000      1.000 0.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1927026     4  0.0000      1.000 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1927024     4  0.0000      1.000 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1927025     5  0.0000      1.000 0.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1927023     5  0.0000      1.000 0.000 0.000 0.000 0.000  1 0.000
#&gt; SRR1927022     4  0.0000      1.000 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1927021     6  0.0000      0.958 0.000 0.000 0.000 0.000  0 1.000
#&gt; SRR1927020     4  0.0000      1.000 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1927019     2  0.0000      0.975 0.000 1.000 0.000 0.000  0 0.000
#&gt; SRR1927071     4  0.0000      1.000 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1927069     6  0.0000      0.958 0.000 0.000 0.000 0.000  0 1.000
#&gt; SRR1927070     1  0.0146      0.995 0.996 0.000 0.000 0.004  0 0.000
#&gt; SRR1927068     4  0.0000      1.000 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1927066     4  0.0000      1.000 0.000 0.000 0.000 1.000  0 0.000
#&gt; SRR1927065     3  0.0000      0.950 0.000 0.000 1.000 0.000  0 0.000
#&gt; SRR1927067     3  0.0000      0.950 0.000 0.000 1.000 0.000  0 0.000
#&gt; SRR1927064     1  0.0000      1.000 1.000 0.000 0.000 0.000  0 0.000
#&gt; SRR1927063     2  0.0000      0.975 0.000 1.000 0.000 0.000  0 0.000
#&gt; SRR1927062     4  0.0000      1.000 0.000 0.000 0.000 1.000  0 0.000
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-5-a').click(function(){
  $('#tab-ATC-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-signatures'>
<ul>
<li><a href='#tab-ATC-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-1-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-1"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-2-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-2"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-3-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-3"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-4-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-4"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-5-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-mclust-signature_compare](figure_cola/ATC-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-mclust-collect-classes](figure_cola/ATC-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:NMF*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "NMF"]
# you can also extract it by
# res = res_list["ATC:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16868 rows and 52 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-NMF-collect-plots](figure_cola/ATC-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-NMF-select-partition-number](figure_cola/ATC-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5095 0.491   0.491
#> 3 3 0.917           0.883       0.951         0.2624 0.864   0.724
#> 4 4 0.715           0.723       0.875         0.1198 0.858   0.631
#> 5 5 0.693           0.663       0.806         0.0571 0.922   0.731
#> 6 6 0.671           0.534       0.758         0.0388 0.883   0.579
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-classes'>
<ul>
<li><a href='#tab-ATC-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-NMF-get-classes-1'>
<p><a id='tab-ATC-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1927048     1       0          1  1  0
#&gt; SRR1927061     2       0          1  0  1
#&gt; SRR1927060     1       0          1  1  0
#&gt; SRR1927059     2       0          1  0  1
#&gt; SRR1927058     1       0          1  1  0
#&gt; SRR1927057     2       0          1  0  1
#&gt; SRR1927055     2       0          1  0  1
#&gt; SRR1927056     1       0          1  1  0
#&gt; SRR1927054     1       0          1  1  0
#&gt; SRR1927052     1       0          1  1  0
#&gt; SRR1927053     2       0          1  0  1
#&gt; SRR1927051     2       0          1  0  1
#&gt; SRR1927050     1       0          1  1  0
#&gt; SRR1927049     2       0          1  0  1
#&gt; SRR1927047     2       0          1  0  1
#&gt; SRR1927046     1       0          1  1  0
#&gt; SRR1927045     2       0          1  0  1
#&gt; SRR1927044     1       0          1  1  0
#&gt; SRR1927043     2       0          1  0  1
#&gt; SRR1927042     1       0          1  1  0
#&gt; SRR1927040     1       0          1  1  0
#&gt; SRR1927039     2       0          1  0  1
#&gt; SRR1927038     1       0          1  1  0
#&gt; SRR1927037     2       0          1  0  1
#&gt; SRR1927036     1       0          1  1  0
#&gt; SRR1927035     2       0          1  0  1
#&gt; SRR1927034     1       0          1  1  0
#&gt; SRR1927033     2       0          1  0  1
#&gt; SRR1927032     1       0          1  1  0
#&gt; SRR1927031     2       0          1  0  1
#&gt; SRR1927030     1       0          1  1  0
#&gt; SRR1927028     1       0          1  1  0
#&gt; SRR1927029     2       0          1  0  1
#&gt; SRR1927027     2       0          1  0  1
#&gt; SRR1927026     1       0          1  1  0
#&gt; SRR1927024     1       0          1  1  0
#&gt; SRR1927025     2       0          1  0  1
#&gt; SRR1927023     2       0          1  0  1
#&gt; SRR1927022     1       0          1  1  0
#&gt; SRR1927021     2       0          1  0  1
#&gt; SRR1927020     1       0          1  1  0
#&gt; SRR1927019     2       0          1  0  1
#&gt; SRR1927071     1       0          1  1  0
#&gt; SRR1927069     2       0          1  0  1
#&gt; SRR1927070     1       0          1  1  0
#&gt; SRR1927068     1       0          1  1  0
#&gt; SRR1927066     1       0          1  1  0
#&gt; SRR1927065     2       0          1  0  1
#&gt; SRR1927067     2       0          1  0  1
#&gt; SRR1927064     1       0          1  1  0
#&gt; SRR1927063     2       0          1  0  1
#&gt; SRR1927062     1       0          1  1  0
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-1-a').click(function(){
  $('#tab-ATC-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-2'>
<p><a id='tab-ATC-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1927048     3  0.0000      0.868 0.000 0.000 1.000
#&gt; SRR1927061     2  0.0000      0.979 0.000 1.000 0.000
#&gt; SRR1927060     3  0.0000      0.868 0.000 0.000 1.000
#&gt; SRR1927059     2  0.0892      0.968 0.000 0.980 0.020
#&gt; SRR1927058     3  0.6126      0.378 0.400 0.000 0.600
#&gt; SRR1927057     2  0.0000      0.979 0.000 1.000 0.000
#&gt; SRR1927055     2  0.0000      0.979 0.000 1.000 0.000
#&gt; SRR1927056     1  0.0000      0.933 1.000 0.000 0.000
#&gt; SRR1927054     3  0.0892      0.864 0.020 0.000 0.980
#&gt; SRR1927052     1  0.1411      0.914 0.964 0.000 0.036
#&gt; SRR1927053     2  0.2625      0.908 0.000 0.916 0.084
#&gt; SRR1927051     2  0.0237      0.978 0.000 0.996 0.004
#&gt; SRR1927050     1  0.0000      0.933 1.000 0.000 0.000
#&gt; SRR1927049     2  0.0000      0.979 0.000 1.000 0.000
#&gt; SRR1927047     2  0.0747      0.971 0.000 0.984 0.016
#&gt; SRR1927046     3  0.1031      0.863 0.024 0.000 0.976
#&gt; SRR1927045     2  0.0000      0.979 0.000 1.000 0.000
#&gt; SRR1927044     3  0.6204      0.313 0.424 0.000 0.576
#&gt; SRR1927043     2  0.0000      0.979 0.000 1.000 0.000
#&gt; SRR1927042     3  0.1031      0.863 0.024 0.000 0.976
#&gt; SRR1927040     3  0.0000      0.868 0.000 0.000 1.000
#&gt; SRR1927039     2  0.5706      0.560 0.000 0.680 0.320
#&gt; SRR1927038     3  0.0000      0.868 0.000 0.000 1.000
#&gt; SRR1927037     2  0.0237      0.978 0.000 0.996 0.004
#&gt; SRR1927036     3  0.5988      0.448 0.368 0.000 0.632
#&gt; SRR1927035     2  0.0000      0.979 0.000 1.000 0.000
#&gt; SRR1927034     1  0.0000      0.933 1.000 0.000 0.000
#&gt; SRR1927033     2  0.0000      0.979 0.000 1.000 0.000
#&gt; SRR1927032     3  0.0000      0.868 0.000 0.000 1.000
#&gt; SRR1927031     2  0.0000      0.979 0.000 1.000 0.000
#&gt; SRR1927030     1  0.5948      0.377 0.640 0.000 0.360
#&gt; SRR1927028     1  0.0000      0.933 1.000 0.000 0.000
#&gt; SRR1927029     2  0.0000      0.979 0.000 1.000 0.000
#&gt; SRR1927027     2  0.0000      0.979 0.000 1.000 0.000
#&gt; SRR1927026     1  0.0000      0.933 1.000 0.000 0.000
#&gt; SRR1927024     1  0.1529      0.911 0.960 0.000 0.040
#&gt; SRR1927025     2  0.0000      0.979 0.000 1.000 0.000
#&gt; SRR1927023     2  0.0592      0.974 0.000 0.988 0.012
#&gt; SRR1927022     1  0.3192      0.842 0.888 0.000 0.112
#&gt; SRR1927021     2  0.1163      0.961 0.000 0.972 0.028
#&gt; SRR1927020     1  0.0000      0.933 1.000 0.000 0.000
#&gt; SRR1927019     2  0.0000      0.979 0.000 1.000 0.000
#&gt; SRR1927071     1  0.0000      0.933 1.000 0.000 0.000
#&gt; SRR1927069     2  0.0237      0.978 0.000 0.996 0.004
#&gt; SRR1927070     1  0.4974      0.664 0.764 0.000 0.236
#&gt; SRR1927068     1  0.0000      0.933 1.000 0.000 0.000
#&gt; SRR1927066     1  0.0000      0.933 1.000 0.000 0.000
#&gt; SRR1927065     2  0.0000      0.979 0.000 1.000 0.000
#&gt; SRR1927067     2  0.0000      0.979 0.000 1.000 0.000
#&gt; SRR1927064     3  0.0000      0.868 0.000 0.000 1.000
#&gt; SRR1927063     2  0.0237      0.978 0.000 0.996 0.004
#&gt; SRR1927062     1  0.0000      0.933 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-2-a').click(function(){
  $('#tab-ATC-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-3'>
<p><a id='tab-ATC-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1927048     1  0.0336     0.8052 0.992 0.000 0.008 0.000
#&gt; SRR1927061     2  0.2011     0.8022 0.000 0.920 0.080 0.000
#&gt; SRR1927060     1  0.0000     0.8058 1.000 0.000 0.000 0.000
#&gt; SRR1927059     2  0.5881     0.4153 0.240 0.676 0.084 0.000
#&gt; SRR1927058     1  0.4072     0.6184 0.748 0.000 0.000 0.252
#&gt; SRR1927057     2  0.1743     0.8423 0.004 0.940 0.056 0.000
#&gt; SRR1927055     2  0.1867     0.8274 0.000 0.928 0.072 0.000
#&gt; SRR1927056     4  0.0000     0.9089 0.000 0.000 0.000 1.000
#&gt; SRR1927054     1  0.0188     0.8064 0.996 0.000 0.000 0.004
#&gt; SRR1927052     4  0.2466     0.8391 0.096 0.000 0.004 0.900
#&gt; SRR1927053     1  0.7386    -0.1182 0.496 0.320 0.184 0.000
#&gt; SRR1927051     2  0.0657     0.8558 0.004 0.984 0.012 0.000
#&gt; SRR1927050     4  0.0000     0.9089 0.000 0.000 0.000 1.000
#&gt; SRR1927049     2  0.0336     0.8556 0.000 0.992 0.008 0.000
#&gt; SRR1927047     2  0.7086    -0.0127 0.160 0.548 0.292 0.000
#&gt; SRR1927046     1  0.1733     0.7943 0.948 0.000 0.028 0.024
#&gt; SRR1927045     2  0.1474     0.8443 0.000 0.948 0.052 0.000
#&gt; SRR1927044     1  0.4072     0.6187 0.748 0.000 0.000 0.252
#&gt; SRR1927043     2  0.0921     0.8549 0.000 0.972 0.028 0.000
#&gt; SRR1927042     1  0.0336     0.8060 0.992 0.000 0.000 0.008
#&gt; SRR1927040     1  0.0188     0.8050 0.996 0.000 0.004 0.000
#&gt; SRR1927039     1  0.6102     0.3215 0.672 0.212 0.116 0.000
#&gt; SRR1927038     1  0.0000     0.8058 1.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.1411     0.8462 0.020 0.960 0.020 0.000
#&gt; SRR1927036     1  0.4401     0.5866 0.724 0.000 0.004 0.272
#&gt; SRR1927035     2  0.0657     0.8558 0.004 0.984 0.012 0.000
#&gt; SRR1927034     4  0.0000     0.9089 0.000 0.000 0.000 1.000
#&gt; SRR1927033     2  0.0817     0.8566 0.000 0.976 0.024 0.000
#&gt; SRR1927032     1  0.0336     0.8053 0.992 0.000 0.008 0.000
#&gt; SRR1927031     3  0.5695     0.3469 0.024 0.476 0.500 0.000
#&gt; SRR1927030     1  0.5143     0.1228 0.540 0.000 0.004 0.456
#&gt; SRR1927028     4  0.0000     0.9089 0.000 0.000 0.000 1.000
#&gt; SRR1927029     2  0.2216     0.7888 0.000 0.908 0.092 0.000
#&gt; SRR1927027     3  0.3764     0.7886 0.000 0.216 0.784 0.000
#&gt; SRR1927026     4  0.1489     0.8873 0.004 0.000 0.044 0.952
#&gt; SRR1927024     4  0.6033     0.6790 0.116 0.000 0.204 0.680
#&gt; SRR1927025     3  0.2973     0.7844 0.000 0.144 0.856 0.000
#&gt; SRR1927023     3  0.2888     0.7691 0.004 0.124 0.872 0.000
#&gt; SRR1927022     4  0.4874     0.7193 0.180 0.000 0.056 0.764
#&gt; SRR1927021     3  0.5578     0.7061 0.040 0.312 0.648 0.000
#&gt; SRR1927020     4  0.0000     0.9089 0.000 0.000 0.000 1.000
#&gt; SRR1927019     2  0.2021     0.8237 0.012 0.932 0.056 0.000
#&gt; SRR1927071     4  0.0000     0.9089 0.000 0.000 0.000 1.000
#&gt; SRR1927069     2  0.4500     0.3276 0.000 0.684 0.316 0.000
#&gt; SRR1927070     4  0.4933     0.1832 0.432 0.000 0.000 0.568
#&gt; SRR1927068     4  0.0000     0.9089 0.000 0.000 0.000 1.000
#&gt; SRR1927066     4  0.0000     0.9089 0.000 0.000 0.000 1.000
#&gt; SRR1927065     2  0.0817     0.8560 0.000 0.976 0.024 0.000
#&gt; SRR1927067     2  0.1302     0.8486 0.000 0.956 0.044 0.000
#&gt; SRR1927064     1  0.0336     0.8052 0.992 0.000 0.008 0.000
#&gt; SRR1927063     2  0.1520     0.8441 0.020 0.956 0.024 0.000
#&gt; SRR1927062     4  0.0188     0.9071 0.004 0.000 0.000 0.996
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-3-a').click(function(){
  $('#tab-ATC-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-4'>
<p><a id='tab-ATC-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1927048     1  0.0000      0.858 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927061     3  0.1892      0.675 0.000 0.080 0.916 0.000 0.004
#&gt; SRR1927060     1  0.0000      0.858 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927059     3  0.7119     -0.343 0.244 0.360 0.380 0.000 0.016
#&gt; SRR1927058     1  0.1830      0.835 0.924 0.000 0.000 0.068 0.008
#&gt; SRR1927057     3  0.4270      0.446 0.004 0.336 0.656 0.000 0.004
#&gt; SRR1927055     3  0.4847      0.559 0.000 0.240 0.692 0.000 0.068
#&gt; SRR1927056     4  0.0000      0.894 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927054     1  0.0324      0.857 0.992 0.000 0.000 0.004 0.004
#&gt; SRR1927052     4  0.2813      0.839 0.024 0.000 0.000 0.868 0.108
#&gt; SRR1927053     2  0.7156      0.416 0.296 0.456 0.220 0.000 0.028
#&gt; SRR1927051     3  0.2674      0.736 0.000 0.120 0.868 0.000 0.012
#&gt; SRR1927050     4  0.0000      0.894 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927049     3  0.1281      0.733 0.000 0.032 0.956 0.000 0.012
#&gt; SRR1927047     2  0.5724      0.568 0.056 0.628 0.284 0.000 0.032
#&gt; SRR1927046     1  0.3065      0.798 0.872 0.008 0.000 0.048 0.072
#&gt; SRR1927045     3  0.2719      0.728 0.000 0.144 0.852 0.000 0.004
#&gt; SRR1927044     1  0.1768      0.834 0.924 0.000 0.000 0.072 0.004
#&gt; SRR1927043     3  0.3194      0.716 0.000 0.148 0.832 0.000 0.020
#&gt; SRR1927042     1  0.0000      0.858 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927040     1  0.0000      0.858 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927039     1  0.7227     -0.395 0.424 0.364 0.172 0.000 0.040
#&gt; SRR1927038     1  0.0000      0.858 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1927037     3  0.3431      0.722 0.020 0.144 0.828 0.000 0.008
#&gt; SRR1927036     1  0.2966      0.735 0.816 0.000 0.000 0.184 0.000
#&gt; SRR1927035     3  0.3087      0.728 0.004 0.152 0.836 0.000 0.008
#&gt; SRR1927034     4  0.0000      0.894 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927033     3  0.3119      0.685 0.000 0.068 0.860 0.000 0.072
#&gt; SRR1927032     1  0.0162      0.857 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1927031     2  0.4042      0.623 0.012 0.772 0.196 0.000 0.020
#&gt; SRR1927030     1  0.2886      0.771 0.844 0.000 0.000 0.148 0.008
#&gt; SRR1927028     4  0.1894      0.869 0.008 0.000 0.000 0.920 0.072
#&gt; SRR1927029     3  0.2505      0.660 0.000 0.092 0.888 0.000 0.020
#&gt; SRR1927027     2  0.4884      0.486 0.000 0.720 0.128 0.000 0.152
#&gt; SRR1927026     4  0.4147      0.573 0.008 0.000 0.000 0.676 0.316
#&gt; SRR1927024     5  0.3621      0.450 0.020 0.000 0.000 0.192 0.788
#&gt; SRR1927025     2  0.5391      0.379 0.000 0.652 0.116 0.000 0.232
#&gt; SRR1927023     5  0.4869      0.442 0.004 0.344 0.028 0.000 0.624
#&gt; SRR1927022     4  0.5811      0.489 0.140 0.000 0.000 0.596 0.264
#&gt; SRR1927021     5  0.5873      0.300 0.008 0.192 0.168 0.000 0.632
#&gt; SRR1927020     4  0.0000      0.894 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927019     3  0.2228      0.716 0.004 0.076 0.908 0.000 0.012
#&gt; SRR1927071     4  0.0880      0.887 0.000 0.000 0.000 0.968 0.032
#&gt; SRR1927069     2  0.4392      0.405 0.000 0.612 0.380 0.000 0.008
#&gt; SRR1927070     1  0.4161      0.349 0.608 0.000 0.000 0.392 0.000
#&gt; SRR1927068     4  0.0000      0.894 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1927066     4  0.0404      0.891 0.012 0.000 0.000 0.988 0.000
#&gt; SRR1927065     3  0.2605      0.720 0.000 0.148 0.852 0.000 0.000
#&gt; SRR1927067     3  0.4268      0.576 0.000 0.268 0.708 0.000 0.024
#&gt; SRR1927064     1  0.0579      0.852 0.984 0.008 0.000 0.000 0.008
#&gt; SRR1927063     3  0.2141      0.721 0.004 0.064 0.916 0.000 0.016
#&gt; SRR1927062     4  0.2414      0.818 0.080 0.008 0.000 0.900 0.012
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-4-a').click(function(){
  $('#tab-ATC-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-5'>
<p><a id='tab-ATC-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1927048     1  0.0260     0.8886 0.992 0.000 0.000 0.000 0.008 0.000
#&gt; SRR1927061     3  0.3830     0.6894 0.000 0.376 0.620 0.000 0.004 0.000
#&gt; SRR1927060     1  0.0508     0.8882 0.984 0.000 0.004 0.000 0.012 0.000
#&gt; SRR1927059     2  0.5362     0.2056 0.176 0.644 0.012 0.000 0.164 0.004
#&gt; SRR1927058     1  0.4029     0.8041 0.804 0.000 0.048 0.076 0.068 0.004
#&gt; SRR1927057     2  0.5176     0.2574 0.000 0.620 0.192 0.000 0.188 0.000
#&gt; SRR1927055     3  0.5406     0.6332 0.000 0.380 0.500 0.000 0.120 0.000
#&gt; SRR1927056     4  0.0000     0.8544 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927054     1  0.0603     0.8874 0.980 0.000 0.004 0.000 0.016 0.000
#&gt; SRR1927052     4  0.4405     0.7097 0.064 0.000 0.028 0.792 0.068 0.048
#&gt; SRR1927053     2  0.5980     0.0604 0.204 0.544 0.012 0.000 0.236 0.004
#&gt; SRR1927051     2  0.1245     0.4817 0.000 0.952 0.016 0.000 0.032 0.000
#&gt; SRR1927050     4  0.0146     0.8538 0.000 0.000 0.004 0.996 0.000 0.000
#&gt; SRR1927049     2  0.2872     0.3255 0.000 0.836 0.140 0.000 0.024 0.000
#&gt; SRR1927047     2  0.5430     0.0935 0.128 0.600 0.012 0.000 0.260 0.000
#&gt; SRR1927046     1  0.1774     0.8688 0.936 0.004 0.000 0.024 0.016 0.020
#&gt; SRR1927045     2  0.4344    -0.3118 0.000 0.628 0.336 0.000 0.036 0.000
#&gt; SRR1927044     1  0.4303     0.7876 0.784 0.000 0.056 0.088 0.068 0.004
#&gt; SRR1927043     3  0.4409     0.7239 0.000 0.380 0.588 0.000 0.032 0.000
#&gt; SRR1927042     1  0.0291     0.8884 0.992 0.000 0.000 0.004 0.004 0.000
#&gt; SRR1927040     1  0.0363     0.8871 0.988 0.000 0.000 0.000 0.012 0.000
#&gt; SRR1927039     2  0.6152     0.0720 0.252 0.520 0.016 0.000 0.208 0.004
#&gt; SRR1927038     1  0.0000     0.8884 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1927037     2  0.2401     0.4852 0.048 0.900 0.024 0.000 0.028 0.000
#&gt; SRR1927036     1  0.2504     0.8154 0.856 0.004 0.000 0.136 0.004 0.000
#&gt; SRR1927035     2  0.1649     0.4777 0.000 0.932 0.036 0.000 0.032 0.000
#&gt; SRR1927034     4  0.0000     0.8544 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927033     3  0.5112     0.7177 0.000 0.340 0.584 0.000 0.060 0.016
#&gt; SRR1927032     1  0.0458     0.8861 0.984 0.000 0.000 0.000 0.016 0.000
#&gt; SRR1927031     5  0.4128     0.1010 0.004 0.488 0.004 0.000 0.504 0.000
#&gt; SRR1927030     1  0.4818     0.7494 0.744 0.000 0.100 0.084 0.068 0.004
#&gt; SRR1927028     4  0.2026     0.8212 0.004 0.000 0.008 0.916 0.012 0.060
#&gt; SRR1927029     3  0.3636     0.6951 0.000 0.320 0.676 0.000 0.004 0.000
#&gt; SRR1927027     5  0.4591     0.4892 0.000 0.224 0.084 0.000 0.688 0.004
#&gt; SRR1927026     4  0.3868    -0.0713 0.000 0.000 0.000 0.508 0.000 0.492
#&gt; SRR1927024     6  0.1863     0.4991 0.016 0.000 0.004 0.060 0.000 0.920
#&gt; SRR1927025     5  0.6040     0.3795 0.000 0.192 0.016 0.000 0.512 0.280
#&gt; SRR1927023     6  0.4539     0.2510 0.000 0.032 0.016 0.000 0.296 0.656
#&gt; SRR1927022     6  0.5823     0.1228 0.188 0.000 0.000 0.372 0.000 0.440
#&gt; SRR1927021     2  0.6194    -0.2663 0.012 0.412 0.004 0.000 0.172 0.400
#&gt; SRR1927020     4  0.0000     0.8544 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927019     2  0.2218     0.4003 0.000 0.884 0.104 0.000 0.012 0.000
#&gt; SRR1927071     4  0.1874     0.8279 0.000 0.000 0.016 0.928 0.028 0.028
#&gt; SRR1927069     2  0.4123    -0.1920 0.000 0.568 0.012 0.000 0.420 0.000
#&gt; SRR1927070     1  0.4107     0.5999 0.684 0.000 0.000 0.280 0.036 0.000
#&gt; SRR1927068     4  0.0000     0.8544 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1927066     4  0.0260     0.8513 0.008 0.000 0.000 0.992 0.000 0.000
#&gt; SRR1927065     2  0.4210    -0.1370 0.000 0.672 0.288 0.000 0.040 0.000
#&gt; SRR1927067     3  0.4993     0.6097 0.000 0.316 0.600 0.000 0.080 0.004
#&gt; SRR1927064     1  0.1218     0.8722 0.956 0.012 0.004 0.000 0.028 0.000
#&gt; SRR1927063     2  0.2784     0.3566 0.000 0.848 0.124 0.000 0.028 0.000
#&gt; SRR1927062     4  0.5763     0.4140 0.144 0.000 0.156 0.636 0.064 0.000
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-5-a').click(function(){
  $('#tab-ATC-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-signatures'>
<ul>
<li><a href='#tab-ATC-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-1-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-1"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-2-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-2"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-3-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-3"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-4-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-4"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-5-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-NMF-signature_compare](figure_cola/ATC-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-NMF-collect-classes](figure_cola/ATC-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

## Session info


```r
sessionInfo()
```

```
#> R version 3.6.0 (2019-04-26)
#> Platform: x86_64-pc-linux-gnu (64-bit)
#> Running under: CentOS Linux 7 (Core)
#> 
#> Matrix products: default
#> BLAS:   /usr/lib64/libblas.so.3.4.2
#> LAPACK: /usr/lib64/liblapack.so.3.4.2
#> 
#> locale:
#>  [1] LC_CTYPE=en_GB.UTF-8       LC_NUMERIC=C               LC_TIME=en_GB.UTF-8       
#>  [4] LC_COLLATE=en_GB.UTF-8     LC_MONETARY=en_GB.UTF-8    LC_MESSAGES=en_GB.UTF-8   
#>  [7] LC_PAPER=en_GB.UTF-8       LC_NAME=C                  LC_ADDRESS=C              
#> [10] LC_TELEPHONE=C             LC_MEASUREMENT=en_GB.UTF-8 LC_IDENTIFICATION=C       
#> 
#> attached base packages:
#> [1] grid      stats     graphics  grDevices utils     datasets  methods   base     
#> 
#> other attached packages:
#> [1] genefilter_1.66.0    ComplexHeatmap_2.3.1 markdown_1.1         knitr_1.26          
#> [5] GetoptLong_0.1.7     cola_1.3.2          
#> 
#> loaded via a namespace (and not attached):
#>  [1] circlize_0.4.8       shape_1.4.4          xfun_0.11            slam_0.1-46         
#>  [5] lattice_0.20-38      splines_3.6.0        colorspace_1.4-1     vctrs_0.2.0         
#>  [9] stats4_3.6.0         blob_1.2.0           XML_3.98-1.20        survival_2.44-1.1   
#> [13] rlang_0.4.2          pillar_1.4.2         DBI_1.0.0            BiocGenerics_0.30.0 
#> [17] bit64_0.9-7          RColorBrewer_1.1-2   matrixStats_0.55.0   stringr_1.4.0       
#> [21] GlobalOptions_0.1.1  evaluate_0.14        memoise_1.1.0        Biobase_2.44.0      
#> [25] IRanges_2.18.3       parallel_3.6.0       AnnotationDbi_1.46.1 highr_0.8           
#> [29] Rcpp_1.0.3           xtable_1.8-4         backports_1.1.5      S4Vectors_0.22.1    
#> [33] annotate_1.62.0      skmeans_0.2-11       bit_1.1-14           microbenchmark_1.4-7
#> [37] brew_1.0-6           impute_1.58.0        rjson_0.2.20         png_0.1-7           
#> [41] digest_0.6.23        stringi_1.4.3        polyclip_1.10-0      clue_0.3-57         
#> [45] tools_3.6.0          bitops_1.0-6         magrittr_1.5         eulerr_6.0.0        
#> [49] RCurl_1.95-4.12      RSQLite_2.1.4        tibble_2.1.3         cluster_2.1.0       
#> [53] crayon_1.3.4         pkgconfig_2.0.3      zeallot_0.1.0        Matrix_1.2-17       
#> [57] xml2_1.2.2           httr_1.4.1           R6_2.4.1             mclust_5.4.5        
#> [61] compiler_3.6.0
```


