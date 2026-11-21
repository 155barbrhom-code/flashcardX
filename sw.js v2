const V='sadis-v1',SHELL=['./','index.html','manifest.webmanifest','icon-192.png','icon-512.png'];
self.addEventListener('install',e=>{e.waitUntil(caches.open(V).then(c=>c.addAll(SHELL)).then(()=>self.skipWaiting()))});
self.addEventListener('activate',e=>{e.waitUntil(caches.keys().then(k=>Promise.all(k.filter(x=>x!==V&&x!=='fonts').map(x=>caches.delete(x)))).then(()=>self.clients.claim()))});
self.addEventListener('fetch',e=>{const r=e.request;if(r.method!=='GET')return;const u=new URL(r.url);
if(/fonts\.(googleapis|gstatic)\.com$/.test(u.hostname)){e.respondWith(caches.open('fonts').then(async c=>{const m=await c.match(r);const n=fetch(r).then(x=>{if(x.ok||x.type==='opaque')c.put(r,x.clone());return x}).catch(()=>m);return m||n}));return}
if(u.origin===location.origin)e.respondWith(caches.match(r).then(m=>m||fetch(r).then(x=>{const cl=x.clone();caches.open(V).then(c=>c.put(r,cl));return x})).catch(()=>caches.match('index.html')))});
