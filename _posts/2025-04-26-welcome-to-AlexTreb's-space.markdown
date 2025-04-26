<div id="container">
  <div class="inner">

    <header>
      <h2>{{ page.description | default: site.description | default: site.github.project_tagline }}</h2>
    </header>
    <section id="downloads" class="clearfix">
      {% if site.show_downloads %}
      <a href="{{ site.github.zip_url }}" id="download-zip" class="button"><span>Download .zip</span></a>
      <a href="{{ site.github.tar_url }}" id="download-tar-gz" class="button"><span>Download .tar.gz</span></a>
      {% endif %}
{% if site.github.public %}
{% if site.github.is_project_page %}
      <a href="{{ site.github.repository_url }}" id="view-on-github" class="button"><span>View on GitHub</span></a>
{% else %}
      <a href="{{ site.github.owner_url }}" id="view-on-github" class="button"><span>View on GitHub</span></a>
{% endif %}
{% endif %}
    </section>
    <hr>
    <section id="main_content">
      {{ content }}
    </section>

    <footer>
    {% if site.github.is_project_page %}
      {{ site.title | default: site.github.repository_name }} is maintained by <a href="{{ site.github.owner_url }}">{{ site.github.owner_name }}</a><br>
    {% endif %}
