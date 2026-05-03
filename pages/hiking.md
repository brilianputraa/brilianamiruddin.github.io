---
layout: page
title: Hiking
permalink: /hiking/
---

A map of Korean mountains and national parks I've explored. Click on markers to see details.

<div id="hiking-map" aria-label="Map of Korean mountains hiked by Brilian Amiruddin" role="img"></div>

<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/lightbox2/2.11.4/css/lightbox.min.css" />
<script src="https://cdnjs.cloudflare.com/ajax/libs/lightbox2/2.11.4/js/lightbox.min.js"></script>
<script src="{{ '/assets/js/trails.js' | relative_url }}"></script>

<noscript>
<p><em>Map requires JavaScript. Mountains hiked: Geumjeongsan, Bukhansan, Seoraksan, Hallyeohaesang, Byeonsanbando, Jirisan, Hallasan, Gayasan, Mudeungsan, Taebaeksan, Deogyusan, Juwangsan, Namsan (Gyeongju), Woraksan.</em></p>
</noscript>

<style>
#hiking-map {
  height: min(400px, 50vh);
  width: 100%;
  margin: 2rem 0;
  border-radius: 4px;
  background: #f5f5f5;
}
#hiking-map::before {
  content: "Loading map...";
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
  color: #666;
  font-size: 0.9rem;
}
.map-loaded::before { display: none; }
</style>

<script>
document.addEventListener('DOMContentLoaded', function() {
  var mapEl = document.getElementById('hiking-map');
  mapEl.classList.add('map-loaded');
  
  var map = L.map('hiking-map').fitBounds([[34.5, 126.0], [38.5, 130.0]]);
  
  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '&copy; <a href="https://openstreetmap.org">OpenStreetMap</a>'
  }).addTo(map);

  // Mountains data - true = hiked, false = to explore, excluded = not visited
  var mountains = [
    {n:"Geumjeongsan", lat:35.267, lng:129.05, h:true},
    {n:"Bukhansan", lat:37.658, lng:127.043, h:true},
    {n:"Seoraksan", lat:38.117, lng:128.467, h:true},
    {n:"Cheonggyesan", lat:37.416, lng:127.041, h:true},
    {n:"Jirisan", lat:35.335, lng:127.733, h:true},
    {n:"Hallasan", lat:33.362, lng:126.533, h:true},
    {n:"Gayasan", lat:35.822, lng:128.135, h:true},
    {n:"Naejangsan", lat:35.493, lng:126.892, ex:true},
    {n:"Mudeungsan", lat:35.131, lng:127.022, h:true},
    {n:"Taebaeksan", lat:37.083, lng:128.983, h:true},
    {n:"Deogyusan", lat:35.857, lng:127.783, h:true},
    {n:"Juwangsan", lat:36.397, lng:129.143, h:true},
    {n:"Namsan (Gyeongju)", lat:35.838, lng:129.208, h:true},
    {n:"Woraksan", lat:36.783, lng:128.208, h:true},
    {n:"Hallyeohaesang", lat:34.85, lng:128.43, h:true},
    {n:"Byeonsanbando", lat:35.68, lng:126.58, h:true},
    // Not hiked - excluded parks
    {n:"Sobaeksan", lat:36.977, lng:128.383, ex:true},
    {n:"Songnisan", lat:36.577, lng:127.883, ex:true},
    {n:"Odaesan", lat:37.783, lng:128.55, ex:true},
    {n:"Wolchulsan", lat:35.283, lng:126.717, ex:true},
    {n:"Palgongsan", lat:36.033, lng:128.617, ex:true},
    {n:"Gyeryongsan", lat:36.35, lng:127.2, ex:true},
    {n:"Chiaksan", lat:37.217, lng:128.05, ex:true},
    // Other mountains
    {n:"Sinbulsan", lat:35.583, lng:129.183},
    {n:"Ganwolsan", lat:35.55, lng:129.25},
    {n:"Gwanaksan", lat:37.45, lng:127.017},
    {n:"Jangtaesan (Daejeon)", lat:36.35, lng:127.35, h:true},
    {n:"Mireuksan", lat:36.333, lng:127.933},
    {n:"Daedunsan", lat:36.35, lng:127.333},
    {n:"Hwangnyeongsan", lat:35.183, lng:129.05},
    {n:"Banyasan", lat:36.183, lng:127.1},
    // Gunsan - Gogunsan area
    {n:"Namaksan (Gogunsan)", lat:35.98, lng:126.73},
    {n:"Daejangbong (Gogunsan)", lat:36.0, lng:126.75}
  ];

  // Hike data from Jekyll collection with photos
  var hikeData = {
    {% for hike in site.hikes %}
    "{{ hike.title }}": {
      photo: "{{ hike.photos[0] | default: '' }}",
      date: "{{ hike.date | date: '%b %Y' }}",
      url: "{{ hike.url | relative_url }}"
    }{% unless forloop.last %},{% endunless %}
    {% endfor %}
  };

  // Icons with larger touch targets (18px for mobile)
  mountains.forEach(function(m) {
    var status = m.h ? 'Hiked' : (m.ex ? 'Not visited' : 'To explore');
    var colorClass = m.h ? 'hiked' : (m.ex ? 'excluded' : 'explore');
    
    var icon = L.divIcon({
      html: '<span class="marker-' + colorClass + '" title="' + m.n + ': ' + status + '"></span>',
      iconSize: [18, 18],
      className: 'mountain-marker'
    });
    
    var popupContent = '<strong>' + m.n + '</strong><br><small>' + status + '</small>';
    
    // Add photo for hiked mountains with lightbox
    if (m.h && hikeData[m.n] && hikeData[m.n].photo) {
      popupContent = '<a href="' + hikeData[m.n].photo + '" data-lightbox="hikes" data-title="' + m.n + '" style="display:block;text-decoration:none;"><img src="' + hikeData[m.n].photo + '" style="width:200px;height:150px;object-fit:cover;border-radius:12px;display:block;margin:0 auto 8px;box-shadow:0 2px 8px rgba(0,0,0,0.15);"><strong style="display:block;text-align:center;font-size:16px;color:#222;">' + m.n + '</strong></a>';
    }
    
    L.marker([m.lat, m.lng], {icon: icon}).addTo(map)
      .bindPopup(popupContent);
  });

  // Add coastal trail polylines
  if (typeof TRAILS !== 'undefined') {
    var trailStyle = {
      color: '#28a745',
      weight: 3,
      opacity: 0.7,
      dashArray: '10, 5'
    };

    Object.entries(TRAILS).forEach(function([key, trail]) {
      L.polyline(trail.coords, trailStyle)
        .bindPopup('<strong>' + trail.name + '</strong><br><small>' + trail.desc + '</small>')
        .addTo(map);
    });
  }
});
</script>

<style>
.mountain-marker span {
  display: block;
  width: 18px;
  height: 18px;
  border-radius: 50%;
  border: 2px solid;
  cursor: pointer;
}
.marker-hiked { background: #28a745; border-color: #fff; }
.marker-explore { background: #0366d6; border-color: #fff; }
.marker-excluded { background: #d1d5da; border-color: #d1d5da; opacity: 0.6; }

/* Trail polyline styles */
.leaflet-overlay-pane path {
  stroke-linecap: round;
  stroke-linejoin: round;
}
</style>

**Mountains I've hiked:**

- Geumjeongsan (Busan) - January 2025
- Bukhansan (Seoul) - To add date
- Seoraksan (Gangwon) - To add date
- Cheonggyesan (Seoul) - To add date
- Jangtaesan (Daejeon) - To add date
- Hallyeohaesang (Tongyeong/Yeosu) - To add date
- Byeonsanbando (Jeollabuk-do) - To add date
- Jirisan - To add date
- Hallasan - To add date
- Gayasan - To add date
- Mudeungsan - To add date
- Taebaeksan - To add date
- Deogyusan - To add date
- Juwangsan - To add date
- Namsan (Gyeongju) - To add date
- Woraksan - To add date

**Not visited yet:**

- Sobaeksan, Songnisan, Odaesan, Wolchulsan, Palgongsan, Gyeryongsan, Chiaksan, Naejangsan

---

## Trailing in Korea

Korea has an extensive network of long-distance coastal trails. I've completed sections of two major southern coastal trails:

**Haeparanggil (East Sea Trail)** - Total 770km along Korea's eastern coastline

- ✅ Course 1: Busan (Songjeong → Haeundae)
- ✅ Course 2: Busan (Haeundae → Dongnae)
- ✅ Course 3: Busan (Dongnae → Gijang)
- ✅ Course 4: Busan/Gijang (Gijang → Jangsan)
- Remaining: Courses 5-20 (Ulsan → Gangwon → Sokcho)

**Namparanggil (South Sea Trail)** - Total 1,463km along Korea's southern coastline

- ✅ Course 2: Busan (Yeongdo → Nampo-dong)
- ✅ Course 4: Busan (Songjeong → Dadaepo)
- ✅ Course 5: Busan/Changwon (Dadaepo → Jinhae)
- Remaining: Courses 1, 3, 6-21 (Mokpo → Tongyeong → Busan)