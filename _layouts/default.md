<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="pt-pt">
<head>
  <meta http-equiv="content-type" content="text/html; charset=utf-8" />
  <title>(in)conception</title>
  <meta name="author" content="" />

  <!-- syntax highlighting CSS -->
  <link rel="stylesheet" href="/assets/css/common.css" type="text/css" />
  <link rel="stylesheet" href="/assets/css/default.css" type="text/css" />
  {% for css in layout.css %}
    <link rel="stylesheet" href="{{css}}" type="text/css" />
  {% endfor %}
</head>

<body>

{{content}}

<!-- Google Analytics -->
<script type="text/javascript">
  var _gaq = _gaq || [];
  _gaq.push(['_setAccount', 'UA-39386601-1']);
  _gaq.push(['_setDomainName', 'islandofatlas.net']);
  _gaq.push(['_trackPageview']);

  (function() {
    var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
    ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'http://www') + '.google-analytics.com/ga.js';
    var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
  })();
</script>
<!-- /Google Analytics -->

</body>
</html>
