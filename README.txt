MAD-K CONFIGURATOR — SETUP NOTES
================================

WHAT'S IN THIS FOLDER
---------------------
index.html                The whole configurator: page layout, styles and code in one file.
models/mk4-10in.json      10in frame, converted from your STEP file.
models/source1-5in.json   5in frame, converted from your STL file.
vendor/three-bundle.js    Backup copy of three.js, the 3D engine. The page loads
                          three.js from cdn.jsdelivr.net and only uses this file
                          if that's blocked.

The .json files are 3D models in glTF format, the standard 3D format for
web browsers. The page loads them from the "models" folder next to it,
so keep the folder structure exactly as it is.


PUT IT ON DECISIVEDRONES.COM
----------------------------
Recommended: upload the folder as its own page.

1. Log in to your web host's control panel and open File Manager
   (or use an FTP app such as FileZilla).
2. Open the folder that holds WordPress. It's usually "public_html";
   you'll know it's the right one because it contains "wp-content".
3. Upload the whole "mad-k-configurator" folder into it.
4. Visit https://decisivedrones.com/mad-k-configurator/ to check it.
5. In WordPress, add a menu link to that address
   (Appearance > Menus > Custom Links, or your header builder).

Why not the WordPress Media Library? WordPress blocks .json uploads by
default, and the page needs its models in a folder beside it.

Option B, show it inside an existing WordPress page:
add a "Custom HTML" block with this line:

  <iframe src="/mad-k-configurator/" style="width:100%;height:90vh;border:0" title="MAD-K configurator"></iframe>


CHANGE PRICES AND OPTIONS
-------------------------
Open index.html in a text editor (VS Code, or "Edit" in File Manager)
and search for "SETTINGS". Everything you'd normally change is in that
block near the top of the code:

  SIZES   base price for each frame size
  OPTS    every option. "price" is the change from the base price
          (-10 means $10 less). ndaa: true shows the green NDAA badge,
          false shows the red Non-NDAA badge.

Prices you still need to fill in are marked "price TBD"
(C2 links, GPS, 5W VTX). The second-thermal-camera prices
(second: 780 and second: 1380) are placeholders too.

Save the file and upload it again to replace the old one.


REPLACE THE 8IN AND 15IN PLACEHOLDERS
-------------------------------------
Upload a photo (to the Media Library is fine for images), copy its URL,
and put it in that size's line, for example:

  { id: '8', label: '8in', price: 1375, model: '', image: 'https://decisivedrones.com/wp-content/uploads/2026/10/mad-k-8in.webp' },

A 3D model for those sizes also needs the motor, camera and antenna
mounting points measured from the CAD file (the "RIGS" section).


PICK A STYLE
------------
The top bar has a Site / Clean / Tactical switch so you can compare.
Once you choose, set these two lines in SETTINGS:

  showStylePicker: false,
  defaultStyle: 'site',      ('site', 'clean' or 'tactical')


QUOTE REQUESTS
--------------
"Request a quote" opens the customer's email app with the full build
filled in, addressed to sales@decisivedrones.com. If they don't use an
email app, the page shows the request with a Copy button and your
address.

To get requests without the email-app step, set quoteEndpoint to a form
service URL (Formspree, a WordPress forms plugin endpoint, etc.). The
page sends name, email, phone, unit, quantity, notes, build code, price
and a text summary as JSON.


GOOD TO KNOW
------------
- Every build has a code like MK-10-h7n-bf-day.thn-3w-crsfd-gpsn.
  Adding "#" plus the code to the page address reopens that exact build.
- The 3D engine (three.js) loads from cdn.jsdelivr.net, with the copy
  in "vendor" as a backup. Fonts load from Google Fonts.
- Your site's heading font (Trump Gothic) is licensed and isn't on
  Google Fonts, so the page uses Oswald, a close match. To switch to
  Trump Gothic, copy the @font-face rule for it from your theme's CSS
  into the page's <style> block.
