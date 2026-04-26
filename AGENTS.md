# Adding a New Video

To add a new video (talk, keynote, or podcast) to this repository, you need to update two files: `index.html` and `atom.xml`. 

## 1. Update `index.html`

Add a new `<li>` element inside the `<ol class="talks">` list. The new entry should be added at the **top** of the list (right after `<ol class="talks">`).

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

*   **`type`**: Can be `talk`, `keynote`, or `podcast`.
*   **`VIDEO_ID`**: The YouTube video ID.
*   **`TITLE`**: The title of the talk.
*   **`EVENT`**: The name of the event (e.g., "Cloud Next 2025", "Google I/O 2025").

*(Note: If adding a podcast or a video not hosted on YouTube, you may need to provide a custom image path in the `<img src="...">` tag, similar to existing podcast entries).*

## 2. Update `atom.xml`

Add a new `<entry>` block to the Atom feed. The new entry should be placed at the **top** of the feed entries, immediately preceding the existing `<entry>` tags. Also, remember to update the `<updated>` timestamp of the main feed.

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

*   **`VIDEO_ID`**: The YouTube video ID or the URL of the talk/podcast.
*   **`TITLE`**: The title of the talk.
*   **`YYYY-MM-DD`**: The date the talk was given or published.
*   **`EVENT`**: The name of the event.

**Update main feed timestamp:**
Find the main `<updated>` tag near the top of the file (before the first `<entry>`) and update it to the current date or the date of the new video:
```xml
  <updated>YYYY-MM-DDT00:00:00Z</updated>
```
