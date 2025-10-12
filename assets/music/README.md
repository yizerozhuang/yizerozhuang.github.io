# Music Assets

This directory contains music files and artwork for the music player.

## File Structure

- `default-album.jpg` - Default album artwork for tracks without cover art
- `*.mp3` - Audio files (offline music)
- `*.jpg` - Album artwork images

## Adding Music

1. **For offline music**: Place your `.mp3` files in this directory
2. **For online music**: Update the `audio` field in the playlist to point to online URLs
3. **Album artwork**: Add corresponding `.jpg` files for album covers
4. **Update playlist**: Edit the playlist array in `/music/index.md` to include your tracks

## Supported Audio Formats

- MP3 (recommended for compatibility)
- WAV
- OGG (limited browser support)

## File Naming Convention

- Audio files: `track-name.mp3`
- Artwork: `album-name.jpg`
- Use lowercase with hyphens for consistency

## Example Playlist Entry

```javascript
{
  id: 7,
  title: "Your Song Title",
  artist: "Artist Name",
  album: "Album Name",
  duration: "3:45",
  artwork: "/assets/music/your-album.jpg",
  audio: "/assets/music/your-song.mp3", // or online URL
  genre: "jazz", // or "classical", "other"
  year: "2024"
}
```
