# Updating a Pollinator's Picture

This guide is for replacing the illustration for an existing pollinator in the app. You do not need any programming knowledge to do this. You will use an image editor you already know — like Photoshop, GIMP, or Figma.

When you are done, you will hand one updated image file to your developer. That is the only file that needs to change.

---

## What you need before you start

- Your new illustration, **100 × 100 pixels**, saved as a **PNG with a transparent background** (not JPEG, not PNG with a white background)
- An image editor that can open and export PNG files with transparency (Photoshop, GIMP, Figma, Affinity Photo, etc.)
- The current spritesheet file from your developer or the project folder:
  ```
  Pollinator-Habitat/frontend/public/images/spritesheet_transparent.png
  ```

If you do not have access to the spritesheet file, ask your developer to send it to you.

---

## How the images are stored

All of the pollinator pictures in the app live together in **one single image file** called a spritesheet. Think of it like a sheet of postage stamps — each "stamp" is one illustration, arranged in a grid. The grid is made up of rows (going down) and columns (going across). Each stamp is exactly **100 pixels wide and 100 pixels tall**.

When you update a pollinator's picture, you are replacing one stamp on the sheet, leaving all the others exactly as they are.

---

## Step 1 — Find your pollinator's position on the grid

Use the table below to find the row and column number for the pollinator you want to update.

| Pollinator  | Row | Column |
|-------------|-----|--------|
| Human       | 4   | 0      |
| Hummingbird | 4   | 2      |
| Sunbird     | 4   | 3      |
| Beetle      | 4   | 8      |
| Bat         | 5   | 0      |
| Moth        | 5   | 1      |
| Butterfly   | 5   | 2      |
| Fly         | 5   | 3      |
| Ant         | 3   | 4      |
| Bee         | 6   | 0      |
| Wasp        | 6   | 1      |

---

## Step 2 — Calculate the pixel position

Each cell is 100 × 100 pixels. To find where your pollinator's cell starts in the image, multiply:

```
How far down from the top  =  Row number  × 100
How far in from the left   =  Column number × 100
```

**Examples:**

| Pollinator | Row × 100 | Column × 100 | Cell starts at |
|------------|-----------|--------------|----------------|
| Bat        | 5 × 100 = 500px down | 0 × 100 = 0px from left | Left edge, 500px down |
| Butterfly  | 5 × 100 = 500px down | 2 × 100 = 200px from left | 200px from left, 500px down |
| Bee        | 6 × 100 = 600px down | 0 × 100 = 0px from left | Left edge, 600px down |
| Ant        | 3 × 100 = 300px down | 4 × 100 = 400px from left | 400px from left, 300px down |

---

## Step 3 — Open the spritesheet in your image editor

Open the file `spritesheet_transparent.png` in Photoshop, GIMP, or whichever image editor you are using. **Do not resize the image or crop it** — you are only replacing one cell.

**Tip:** Turn on a grid in your image editor set to 100-pixel spacing. This will draw visible lines at every cell boundary and make it easy to see exactly where each pollinator lives.
- **Photoshop:** View → Show → Grid. Then Edit → Preferences → Guides, Grid & Slices → set Gridline Every: 100 pixels.
- **GIMP:** Image → Configure Grid → set Width and Height to 100px. Then View → Show Grid.

---

## Step 4 — Navigate to the correct cell

Scroll or zoom to the position you calculated in Step 2.

Use your editor's selection tool set to a **fixed size of 100 × 100 pixels**. Click at the pixel position you calculated — this selects the exact 100 × 100 area for your pollinator.

Double-check by looking at what is currently in that cell. It should be the pollinator you intend to replace.

---

## Step 5 — Replace the illustration

Delete the current illustration inside the selected area (or paste your new one directly on top of it). Make sure:

- Your new illustration fits entirely within the 100 × 100 pixel box
- It does not overlap any neighboring cells
- The background of the new illustration is **transparent** — if you see a white box or any colored background behind your artwork, remove it before placing it here

---

## Step 6 — Save the file

Export the updated image as:
- **File format:** PNG
- **Transparency:** Yes (sometimes called "Alpha channel" or "Save with transparency")
- **File name:** `spritesheet_transparent.png` (exactly — do not rename it)

Do not save as JPEG. JPEG does not support transparency and the silhouette effect in the app will break.

---

## Step 7 — Send the file to your developer

Send your developer the updated `spritesheet_transparent.png` file. Tell them:

> "I updated the [pollinator name] picture in the spritesheet. Only the image changed — no text or data was modified. Please deploy the updated spritesheet."

Your developer will place the file in the right folder and redeploy the app. No database changes are needed for an image-only update.

---

## Things to watch out for

**Wrong cell:** Double-check the row and column numbers before you start. If you accidentally edit the wrong cell, you will change a different pollinator's picture or a route-card label.

**White background:** If the new illustration has a white background (not transparent), the silhouette effect on the collection screen will show a white square instead of a black shape. Always use PNG with transparency.

**Resizing the whole image:** Never resize or crop the entire spritesheet. You are only working inside one 100 × 100 cell. The overall image dimensions should stay exactly the same.

**File name:** The file must be saved as exactly `spritesheet_transparent.png`. A different name means the app will not find it.

---

*For technical details about how the spritesheet coordinate system works in code, see the developer guide: `docs/Developer/ADDING_ROUTES.md`.*
