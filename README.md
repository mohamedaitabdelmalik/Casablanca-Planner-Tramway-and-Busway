<div align="center">

<img src="favicon.svg" width="84" alt="Tramway icon">

# Casablanca Planner — Tramway & Busway

**Plan any trip on the Casablanca tramway (T1–T4) and busway (BW1–BW2) in seconds.**
*Calculateur d'itinéraire interactif pour le tramway et le busway de Casablanca.*

[![Live demo](https://img.shields.io/badge/▶_LIVE_DEMO-open_the_app-16a34a?style=for-the-badge)](https://mohamedaitabdelmalik.github.io/Casablanca-Planner-Tramway-and-Busway/)

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![Leaflet](https://img.shields.io/badge/Leaflet-199900?style=flat-square&logo=leaflet&logoColor=white)
![MapLibre GL](https://img.shields.io/badge/MapLibre_GL-396CB2?style=flat-square&logo=maplibre&logoColor=white)
![GitHub Pages](https://img.shields.io/badge/Hosted_on-GitHub_Pages-222?style=flat-square&logo=github&logoColor=white)
![No backend](https://img.shields.io/badge/backend-none-success?style=flat-square)

[**Features**](#-features) · [**How to use**](#-how-to-use) · [**Run locally**](#-run-locally) · [**Deploy**](#-deploy-on-github-pages) · [**How it works**](#-how-it-works) · [**Author**](#-author)

</div>

---

## 🎯 What is it?

Pick a **departure** and an **arrival** station and the app finds the fastest way, with transfers, walking times and the exact section of track you will ride, drawn on an interactive map (flat or **3D**). Share the result on **WhatsApp** or export it as a **PDF**.

> **100 % static.** No server, no database, no account, no API key. Everything runs in your browser, so it is fast and free to host.

## ✨ Features

| | Feature | Details |
|---|---|---|
| 🧭 | **Fastest route** | Shortest-time search across T1–T4 and BW1–BW2, with transfers between lines. |
| 🎯 | **Real track drawing** | Only your A → B section is highlighted, following the real line geometry; the rest of the network is dimmed. |
| 🔁 | **Transfers & walking** | Walking time between connecting stations is included in the total time. |
| 🔤 | **Smart search** | Accent-insensitive autocomplete (*“ain diab”* finds *“Aïn Diab”*) with keyboard navigation (↑ ↓ Enter). |
| 🧊 | **3D map** | Tilted view with 3D buildings (MapLibre GL + OpenFreeMap). |
| 🗺️ | **Base maps** | OpenStreetMap, Esri Satellite, Esri Street, Esri Topo, OpenTopoMap. |
| 📍 | **My position** | Finds the nearest station from your location. |
| 💬 | **WhatsApp sharing** | Sends the trip summary and a link that reopens the same route. |
| 🔗 | **Shareable links** | `?from=Aïn Diab&to=Faculté Ben M'Sick` opens a ready-made itinerary. |
| 📄 | **PDF export** | Printable itinerary with map, steps and a QR code. |
| 🚇 | **Line filter** | Show or hide lines from the legend. |
| 📱 | **Responsive** | Sidebar on desktop, bottom sheet on mobile. |

## 🕹️ How to use

1. Type or pick a **departure station** (or press **📍 My position**).
2. Type or pick an **arrival station** (use **⇅** to swap).
3. Choose a **base map** — or **3D** for the tilted city view.
4. Press **Calculer l'itinéraire**.
5. Read the steps, then **share on WhatsApp** or **download the PDF**.

**Direct link example**

```
https://mohamedaitabdelmalik.github.io/Casablanca-Planner-Tramway-and-Busway/?from=Aïn Diab&to=Faculté Ben M'Sick
```

## 💻 Run locally

```bash
git clone https://github.com/mohamedaitabdelmalik/Casablanca-Planner-Tramway-and-Busway.git
cd Casablanca-Planner-Tramway-and-Busway
python3 -m http.server 8000        # or: npx serve .
```

Open <http://localhost:8000>.

> Don't open `index.html` by double-click: browsers block loading local data files on `file://`.

## 🌍 Deploy on GitHub Pages

1. Push the files to the **root** of the `main` branch.
2. **Settings → Pages → Build and deployment → Source: *Deploy from a branch* → `main` / `(root)` → Save.**
3. After about a minute the site is live at
   `https://<user>.github.io/<repo>/`.

All paths are relative, so it works under `/<repo>/` and on a custom domain. It also runs unchanged on Netlify, Cloudflare Pages or Vercel (no build step, publish directory `.`).

## 🗂️ Project structure

```
index.html        main page
404.html          error page
style.css         responsive styles
router.js         routing engine
app.js            interface, Leaflet map, autocomplete, PDF & WhatsApp
map3d.js          3D map (MapLibre GL)
staticmap.js      map rendering for the PDF
pdf.js            PDF generation
network.dat       network data (encoded)
leaflet.js/.css   Leaflet + marker images (*.png)
favicon.svg
LICENSE           all rights reserved
```

## 🧠 How it works

- **Routing** – the network is turned into a graph. Travel time is computed from the distance along the real track and the line speed, plus a stop penalty; a transfer costs the walking time plus a waiting penalty, so the engine favours fewer transfers.
- **Map drawing** – every step is cut from the real line geometry between its two stations, so the highlighted path follows the rails and not straight segments.
- **3D** – a second MapLibre GL map with extruded buildings shows the same route and stations.
- **PDF** – the map is redrawn on a canvas from base-map tiles and embedded in the PDF with the steps and a QR code.

## ⚠️ Good to know

- Internet is required for map tiles, the 3D map and the CDN libraries (Font Awesome, jsPDF, QRCode).
- If a base map blocks the PDF export, switch to **OpenStreetMap**. The PDF always uses a flat map, even if you are in 3D.
- Travel times are estimates from the network model, not official timetables. Check the operator (Casa Transport / Casa Tramway) for real-time information.

## 🙏 Credits

- Maps: © [OpenStreetMap](https://www.openstreetmap.org/copyright) contributors, [OpenFreeMap](https://openfreemap.org/), Esri, [OpenTopoMap](https://opentopomap.org/)
- Libraries: [Leaflet](https://leafletjs.com/), [MapLibre GL JS](https://maplibre.org/), [jsPDF](https://github.com/parallax/jsPDF), [QRCode.js](https://github.com/davidshimjs/qrcodejs), [Font Awesome](https://fontawesome.com/)

## 👤 Author

**Mohamed AIT ABDELMALIK**
MSc Geoinformatics @ UH2C · Geospatial Data Science, GeoAI & ML · GIS & Remote Sensing · Casablanca Metropolitan Area

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/mohamed-ait-abdelmalik-a7b468195/)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/mohamedaitabdelmalik)
[![X](https://img.shields.io/badge/X-000000?style=flat-square&logo=x&logoColor=white)](https://x.com/MoAitAbdelmalik)

---

## 🇫🇷 En bref

Application web **100 % statique** (HTML + JavaScript) pour calculer un itinéraire sur le **tramway T1–T4** et le **busway BW1–BW2** de Casablanca : tracé réel du tronçon A → B, correspondances, carte **3D**, export **PDF**, partage **WhatsApp** et liens partageables.

**Lancer en local :** `python3 -m http.server 8000` puis ouvrir <http://localhost:8000>
**Publier :** *Settings → Pages → Deploy from a branch → `main` / `(root)`*

## 📄 License

© 2026 Mohamed AIT ABDELMALIK. **All rights reserved.** The code and the network data may not be copied, modified, redistributed or reused without written permission. See [LICENSE](LICENSE).
Third-party components remain under their own licenses.
