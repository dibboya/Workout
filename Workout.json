<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />

  <!-- PWA META -->
  <meta name="theme-color" content="#000000" />
  <link rel="manifest" href="manifest.json" />

  <title>Workout Planner App</title>
  <style>
    body { margin:0; font-family:Arial; background:black; color:white; }
    .container { padding:20px; }
    .day { margin:10px 0; padding:10px; background:#222; border-radius:10px; }
    .exercise { display:flex; margin:5px 0; }
    input { margin-right:10px; }
  </style>
</head>
<body>
<div class="container">
  <h1>Workout App</h1>
  <div id="schedule"></div>
</div>

<script>
if ('serviceWorker' in navigator) {
  navigator.serviceWorker.register('sw.js');
}

const plan = {
  Monday:["Plank 60s","Push-ups x12"],
  Tuesday:["Leg Raises x15","Squats x15"],
  Wednesday:["Rest"],
  Thursday:["Plank 75s","Push-ups x15"],
  Friday:["Core + Legs"],
  Saturday:["Light"],
  Sunday:["Rest"]
};

let progress = JSON.parse(localStorage.getItem('progress'))||{};

function render(){
  const app=document.getElementById('schedule');
  app.innerHTML='';

  Object.keys(plan).forEach(day=>{
    const div=document.createElement('div'); div.className='day';
    div.innerHTML=`<h3>${day}</h3>`;

    plan[day].forEach((ex,i)=>{
      const row=document.createElement('div'); row.className='exercise';
      const cb=document.createElement('input'); cb.type='checkbox';

      if(!progress[day]) progress[day]={};
      cb.checked=progress[day][i]||false;

      cb.onchange=()=>{
        progress[day][i]=cb.checked;
        localStorage.setItem('progress',JSON.stringify(progress));
      };

      row.appendChild(cb);
      row.appendChild(document.createTextNode(ex));
      div.appendChild(row);
    });

    app.appendChild(div);
  });
}

render();
</script>
</body>
</html>


/* manifest.json */
{
  "name": "Workout App",
  "short_name": "Workout",
  "start_url": ".",
  "display": "standalone",
  "background_color": "#000000",
  "theme_color": "#000000",
  "icons": [
    {
      "src": "icon.png",
      "sizes": "192x192",
      "type": "image/png"
    }
  ]
}


/* sw.js */
self.addEventListener('install', e => {
  e.waitUntil(
    caches.open('app').then(cache => cache.addAll(['./']))
  );
});

self.addEventListener('fetch', e => {
  e.respondWith(
    caches.match(e.request).then(res => res || fetch(e.request))
  );
});
