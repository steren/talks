---
name: add-video
description: Instructions for adding a new video (talk, keynote, or podcast) to the repository
---

# Adding a New Video

To add a new video (talk, keynote, or podcast) to this repository, you need to update two files: [index.html](../../../index.html) and [atom.xml](../../../atom.xml). Non-YouTube videos also need a thumbnail image in `images/`.

## 1. Update `index.html`

Add a new `<li>` element inside the `<ol class="talks">` list in [index.html](../../../index.html). The new entry should be added at the **top** of the list (right after `<ol class="talks">`).

**Template for a YouTube video:**

```html
			<li type="talk">
				<a href="https://www.youtube.com/watch?v=VIDEO_ID">
					<figure>
						<img src="https://img.youtube.com/vi/VIDEO_ID/hqdefault.jpg" alt="Video thumbnail">
						<figcaption>
							TITLE
							<br>
							<small>EVENT</small>
						</figcaption>
					</figure>
				</a>
			</li>
```

### Specific Guidance for `index.html`:
*   **`type` attribute**: Must be exactly `talk`, `keynote`, or `podcast` (use the singular form so CSS filters work correctly).
*   **URLs with Timestamps**: For keynotes or specific segments in longer videos, append a timestamp to the YouTube URL (e.g., `&t=2480` or `?feature=shared&t=3976`).
*   **Thumbnails**: 
    *   For standard YouTube videos, use `https://img.youtube.com/vi/VIDEO_ID/hqdefault.jpg`.
    *   For podcasts or videos lacking a good default thumbnail, save a `.webp` image in the `images/` directory and reference it like `src="images/your-custom-image.webp"`. See [Custom thumbnails](#custom-thumbnails) below.
*   **Alt Text**: Include descriptive `alt` text on images, such as `alt="Video thumbnail"` or `alt="Interview thumbnail"`.
*   **`TITLE`**: The title of the talk/podcast.
*   **`EVENT`**: The name of the event (e.g., "Cloud Next 2025", "Google I/O 2025", "Screaming in the cloud").

## 2. Update `atom.xml`

Add a new `<entry>` block to the Atom feed in [atom.xml](../../../atom.xml). The new entry should be placed at the **top** of the feed entries, immediately preceding the existing `<entry>` tags. Also, remember to update the `<updated>` timestamp of the main feed.

**Template for the entry:**

```xml
  <entry>
    <id>https://www.youtube.com/watch?v=VIDEO_ID</id>
    <link rel="alternate" href="https://www.youtube.com/watch?v=VIDEO_ID" />
    <title>TITLE</title>
    <updated>YYYY-MM-DDT00:00:00Z</updated>
    <summary>EVENT</summary>
  </entry>
```

### Specific Guidance for `atom.xml`:
*   **`id` and `link href`**: Use the full URL (e.g., the YouTube link or the podcast URL, including timestamps if applicable).
*   **Escape `&` as `&amp;`** in URLs and titles: a raw `&` makes the whole feed invalid XML.
*   **`summary`**: Use this field for the name of the **event** (e.g., "Cloud Next 2025"), which matches the `<small>` tag in `index.html`.
*   **`TITLE`**: The title of the talk/podcast.
*   **`YYYY-MM-DD`**: The date the talk was given or published.

**Update main feed timestamp:**
Find the main `<updated>` tag near the top of the file (before the first `<entry>`) and update it to the current date or the date of the new video:
```xml
  <updated>YYYY-MM-DDT00:00:00Z</updated>
```

## 3. Custom thumbnails

For videos hosted outside YouTube, grab the thumbnail URL from the video page, then download and convert it to `images/EVENT.webp`:

```bash
curl -sSL -o thumb.jpg "THUMBNAIL_URL"
python -c "from PIL import Image; Image.open('thumb.jpg').convert('RGB').save('images/NAME.webp', 'WEBP', quality=85, method=6)"
```

Look at the image before committing it — auto-generated frames are often black or blurred.

## 4. Verify

```bash
python -c "import xml.dom.minidom; xml.dom.minidom.parse('atom.xml'); print('atom.xml OK')"
```

To check the new card renders, open `index.html` in a browser.
