---
layout: page
title: Traveling
permalink: /traveling/
---

Photos from my travels and adventures.

<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/lightbox2/2.11.4/css/lightbox.min.css" />
<script src="https://cdnjs.cloudflare.com/ajax/libs/lightbox2/2.11.4/js/lightbox.min.js"></script>

<noscript>
<p><em>Photo gallery requires JavaScript.</em></p>
</noscript>

<div class="photo-grid" role="gallery" aria-label="Travel photo gallery">
{% for photo in site.data.travel %}
  <figure class="photo-item">
    <a href="{{ photo.path | relative_url }}" data-lightbox="travel" data-title="{{ photo.alt }} — {{ photo.location }}{% if photo.date %} ({{ photo.date | date: '%b %Y' }}){% endif %}">
      <img src="{{ photo.path | relative_url }}" alt="{{ photo.alt }}" loading="lazy" />
    </a>
    <figcaption>
      <span class="photo-location">{{ photo.location }}</span>
      {% if photo.date %}<span class="photo-date">{{ photo.date | date: '%b %Y' }}</span>{% endif %}
      {% if photo.related_post %}<a class="photo-post-link" href="{{ photo.related_post | relative_url }}">Related post →</a>{% endif %}
    </figcaption>
  </figure>
{% endfor %}
</div>

{% if site.data.travel.size == 0 %}
<div class="photo-empty">
  <div class="photo-empty-icon">📷</div>
  <p>No photos yet.</p>
  <p><small>Add entries to <code>_data/travel.yml</code> to populate this gallery.</small></p>
</div>
{% endif %}

<style>
.photo-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 1rem;
  margin: 2rem 0;
}
.photo-grid img {
  width: 100%;
  height: 250px;
  object-fit: cover;
  border-radius: 4px;
  transition: opacity 0.2s, transform 0.2s;
}
.photo-grid a:hover img { opacity: 0.9; transform: scale(1.02); }
.photo-grid a:focus img { outline: 2px solid #0366d6; }
.photo-grid a {
  display: block;
  background: #f5f5f5;
  border-radius: 4px;
}
.photo-item figcaption {
  padding: 0.5rem 0.25rem;
  font-size: 0.85rem;
  color: #586069;
  line-height: 1.4;
}
.photo-location {
  display: block;
  font-weight: 500;
  color: #333;
}
.photo-date {
  display: inline;
  font-size: 0.8rem;
  color: #888;
}
.photo-post-link {
  display: block;
  color: #0366d6;
  text-decoration: none;
  margin-top: 0.25rem;
  font-size: 0.8rem;
}
.photo-post-link:hover { text-decoration: underline; }
@media (max-width: 800px) {
  .photo-grid { grid-template-columns: repeat(auto-fill, minmax(180px, 1fr)); }
  .photo-grid img { height: 180px; }
}
@media (max-width: 500px) {
  .photo-grid { grid-template-columns: repeat(2, 1fr); gap: 0.5rem; }
  .photo-grid img { height: 150px; }
}
.photo-empty {
  text-align: center;
  padding: 3rem;
  color: #586069;
}
.photo-empty-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
  opacity: 0.5;
}
</style>