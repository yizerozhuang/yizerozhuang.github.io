---
layout: default
title: Music Player
---

<nav>
  <a href="{{ '/' | relative_url }}">Home</a> ·
  <a href="{{ '/blog/' | relative_url }}">Blog</a> ·
  <a href="{{ '/gallery/' | relative_url }}">Photos</a> ·
  <a href="{{ '/resume/' | relative_url }}">Resume</a> ·
  <a href="{{ '/music/' | relative_url }}">Music</a>
  <hr />
</nav>

# 🎵 Music Player

Welcome to my personal music collection! Here you can listen to my favorite tracks, mainly Jazz and other genres I enjoy.

<div id="music-player-container">
  <div class="player-header">
    <h2>Now Playing</h2>
    <div class="current-track-info">
      <div class="track-artwork">
        <img id="current-artwork" src="/assets/music/default-album.jpg" alt="Album Artwork" />
      </div>
      <div class="track-details">
        <h3 id="current-title">Select a track to play</h3>
        <p id="current-artist">Artist</p>
        <p id="current-album">Album</p>
      </div>
    </div>
  </div>

  <div class="player-controls">
    <div class="progress-container">
      <div class="progress-bar">
        <div id="progress" class="progress-fill"></div>
        <div id="progress-handle" class="progress-handle"></div>
      </div>
      <div class="time-display">
        <span id="current-time">0:00</span>
        <span id="total-time">0:00</span>
      </div>
    </div>

    <div class="control-buttons">
      <button id="shuffle-btn" class="control-btn" title="Shuffle">🔀</button>
      <button id="prev-btn" class="control-btn" title="Previous">⏮️</button>
      <button id="play-pause-btn" class="control-btn play-pause" title="Play/Pause">▶️</button>
      <button id="next-btn" class="control-btn" title="Next">⏭️</button>
      <button id="repeat-btn" class="control-btn" title="Repeat">🔁</button>
    </div>

    <div class="volume-control">
      <button id="mute-btn" class="control-btn" title="Mute">🔊</button>
      <div class="volume-slider">
        <input type="range" id="volume" min="0" max="100" value="70" />
      </div>
    </div>
  </div>

  <div class="playlist-section">
    <h3>My Playlist</h3>
    <div class="playlist-filters">
      <button class="filter-btn active" data-filter="all">All</button>
      <button class="filter-btn" data-filter="jazz">Jazz</button>
      <button class="filter-btn" data-filter="classical">Classical</button>
      <button class="filter-btn" data-filter="other">Other</button>
    </div>
    <div id="playlist" class="playlist">
      <!-- Playlist items will be populated by JavaScript -->
    </div>
  </div>
</div>

<audio id="audio-player" preload="metadata"></audio>

<style>
#music-player-container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}

.player-header {
  text-align: center;
  margin-bottom: 30px;
  padding: 20px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border-radius: 15px;
  color: white;
}

.current-track-info {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20px;
  margin-top: 15px;
}

.track-artwork img {
  width: 80px;
  height: 80px;
  border-radius: 10px;
  object-fit: cover;
  box-shadow: 0 4px 15px rgba(0,0,0,0.3);
}

.track-details {
  text-align: left;
}

.track-details h3 {
  margin: 0 0 5px 0;
  font-size: 1.2em;
}

.track-details p {
  margin: 2px 0;
  opacity: 0.8;
  font-size: 0.9em;
}

.player-controls {
  background: #f8f9fa;
  padding: 25px;
  border-radius: 15px;
  margin-bottom: 30px;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}

.progress-container {
  margin-bottom: 20px;
}

.progress-bar {
  position: relative;
  height: 6px;
  background: #e0e0e0;
  border-radius: 3px;
  cursor: pointer;
  margin-bottom: 10px;
}

.progress-fill {
  height: 100%;
  background: linear-gradient(90deg, #667eea, #764ba2);
  border-radius: 3px;
  width: 0%;
  transition: width 0.1s ease;
}

.progress-handle {
  position: absolute;
  top: 50%;
  width: 16px;
  height: 16px;
  background: white;
  border: 2px solid #667eea;
  border-radius: 50%;
  transform: translate(-50%, -50%);
  cursor: pointer;
  opacity: 0;
  transition: opacity 0.2s ease;
}

.progress-bar:hover .progress-handle {
  opacity: 1;
}

.time-display {
  display: flex;
  justify-content: space-between;
  font-size: 0.9em;
  color: #666;
}

.control-buttons {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 15px;
  margin-bottom: 20px;
}

.control-btn {
  background: none;
  border: none;
  font-size: 1.5em;
  cursor: pointer;
  padding: 10px;
  border-radius: 50%;
  transition: all 0.2s ease;
}

.control-btn:hover {
  background: rgba(102, 126, 234, 0.1);
  transform: scale(1.1);
}

.play-pause {
  background: linear-gradient(135deg, #667eea, #764ba2);
  color: white;
  font-size: 2em;
  padding: 15px;
}

.play-pause:hover {
  transform: scale(1.05);
  box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);
}

.volume-control {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
}

.volume-slider {
  width: 100px;
}

.volume-slider input[type="range"] {
  width: 100%;
  height: 4px;
  border-radius: 2px;
  background: #e0e0e0;
  outline: none;
  -webkit-appearance: none;
}

.volume-slider input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 16px;
  height: 16px;
  border-radius: 50%;
  background: #667eea;
  cursor: pointer;
}

.playlist-section {
  background: white;
  border-radius: 15px;
  padding: 25px;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}

.playlist-filters {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
  justify-content: center;
}

.filter-btn {
  padding: 8px 16px;
  border: 2px solid #e0e0e0;
  background: white;
  border-radius: 20px;
  cursor: pointer;
  transition: all 0.2s ease;
  font-size: 0.9em;
}

.filter-btn:hover,
.filter-btn.active {
  background: #667eea;
  color: white;
  border-color: #667eea;
}

.playlist {
  max-height: 400px;
  overflow-y: auto;
}

.playlist-item {
  display: flex;
  align-items: center;
  padding: 12px;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.2s ease;
  margin-bottom: 5px;
}

.playlist-item:hover {
  background: #f8f9fa;
}

.playlist-item.playing {
  background: linear-gradient(90deg, rgba(102, 126, 234, 0.1), rgba(118, 75, 162, 0.1));
  border-left: 4px solid #667eea;
}

.playlist-item .track-number {
  width: 30px;
  text-align: center;
  color: #666;
  font-size: 0.9em;
}

.playlist-item .track-artwork {
  width: 40px;
  height: 40px;
  margin: 0 15px;
  border-radius: 5px;
  object-fit: cover;
}

.playlist-item .track-info {
  flex: 1;
}

.playlist-item .track-title {
  font-weight: 500;
  margin: 0 0 2px 0;
  font-size: 0.95em;
}

.playlist-item .track-artist {
  color: #666;
  margin: 0;
  font-size: 0.85em;
}

.playlist-item .track-duration {
  color: #666;
  font-size: 0.85em;
  margin-left: 15px;
}

@media (max-width: 768px) {
  .current-track-info {
    flex-direction: column;
    text-align: center;
  }
  
  .control-buttons {
    gap: 10px;
  }
  
  .control-btn {
    font-size: 1.2em;
    padding: 8px;
  }
  
  .play-pause {
    font-size: 1.5em;
    padding: 12px;
  }
}
</style>

<script>
// Music Player JavaScript
class MusicPlayer {
  constructor() {
    this.audio = document.getElementById('audio-player');
    this.playlist = [];
    this.currentTrackIndex = 0;
    this.isPlaying = false;
    this.isShuffled = false;
    this.repeatMode = 'none'; // 'none', 'one', 'all'
    this.volume = 0.7;
    
    this.initializeElements();
    this.loadPlaylist();
    this.setupEventListeners();
    this.updateDisplay();
  }

  initializeElements() {
    this.elements = {
      playPauseBtn: document.getElementById('play-pause-btn'),
      prevBtn: document.getElementById('prev-btn'),
      nextBtn: document.getElementById('next-btn'),
      shuffleBtn: document.getElementById('shuffle-btn'),
      repeatBtn: document.getElementById('repeat-btn'),
      muteBtn: document.getElementById('mute-btn'),
      volumeSlider: document.getElementById('volume'),
      progress: document.getElementById('progress'),
      progressHandle: document.getElementById('progress-handle'),
      progressBar: document.querySelector('.progress-bar'),
      currentTime: document.getElementById('current-time'),
      totalTime: document.getElementById('total-time'),
      currentTitle: document.getElementById('current-title'),
      currentArtist: document.getElementById('current-artist'),
      currentAlbum: document.getElementById('current-album'),
      currentArtwork: document.getElementById('current-artwork'),
      playlist: document.getElementById('playlist')
    };
  }

  loadPlaylist() {
    // Sample playlist with both online and offline music
    this.playlist = [
      {
        id: 1,
        title: "Blue in Green",
        artist: "Miles Davis",
        album: "Kind of Blue",
        duration: "5:37",
        artwork: "/assets/music/kind-of-blue.jpg",
        audio: "/assets/music/blue-in-green.mp3", // Offline file
        genre: "jazz",
        year: "1959"
      },
      {
        id: 2,
        title: "Take Five",
        artist: "Dave Brubeck",
        album: "Time Out",
        duration: "5:24",
        artwork: "/assets/music/time-out.jpg",
        audio: "/assets/music/take-five.mp3", // Offline file
        genre: "jazz",
        year: "1959"
      },
      {
        id: 3,
        title: "Autumn Leaves",
        artist: "Cannonball Adderley",
        album: "Something Else",
        duration: "10:59",
        artwork: "/assets/music/something-else.jpg",
        audio: "https://www.soundjay.com/misc/sounds/bell-ringing-05.wav", // Online file (example)
        genre: "jazz",
        year: "1958"
      },
      {
        id: 4,
        title: "Clair de Lune",
        artist: "Claude Debussy",
        album: "Suite Bergamasque",
        duration: "4:47",
        artwork: "/assets/music/suite-bergamasque.jpg",
        audio: "/assets/music/clair-de-lune.mp3", // Offline file
        genre: "classical",
        year: "1905"
      },
      {
        id: 5,
        title: "Giant Steps",
        artist: "John Coltrane",
        album: "Giant Steps",
        duration: "4:45",
        artwork: "/assets/music/giant-steps.jpg",
        audio: "/assets/music/giant-steps.mp3", // Offline file
        genre: "jazz",
        year: "1960"
      },
      {
        id: 6,
        title: "So What",
        artist: "Miles Davis",
        album: "Kind of Blue",
        duration: "9:22",
        artwork: "/assets/music/kind-of-blue.jpg",
        audio: "/assets/music/so-what.mp3", // Offline file
        genre: "jazz",
        year: "1959"
      }
    ];
    
    this.renderPlaylist();
  }

  setupEventListeners() {
    // Play/Pause button
    this.elements.playPauseBtn.addEventListener('click', () => this.togglePlayPause());
    
    // Previous/Next buttons
    this.elements.prevBtn.addEventListener('click', () => this.previousTrack());
    this.elements.nextBtn.addEventListener('click', () => this.nextTrack());
    
    // Shuffle button
    this.elements.shuffleBtn.addEventListener('click', () => this.toggleShuffle());
    
    // Repeat button
    this.elements.repeatBtn.addEventListener('click', () => this.toggleRepeat());
    
    // Mute button
    this.elements.muteBtn.addEventListener('click', () => this.toggleMute());
    
    // Volume slider
    this.elements.volumeSlider.addEventListener('input', (e) => {
      this.setVolume(e.target.value / 100);
    });
    
    // Progress bar
    this.elements.progressBar.addEventListener('click', (e) => {
      const rect = this.elements.progressBar.getBoundingClientRect();
      const clickX = e.clientX - rect.left;
      const percentage = clickX / rect.width;
      this.seekTo(percentage);
    });
    
    // Audio events
    this.audio.addEventListener('timeupdate', () => this.updateProgress());
    this.audio.addEventListener('ended', () => this.handleTrackEnd());
    this.audio.addEventListener('loadedmetadata', () => this.updateDisplay());
    
    // Filter buttons
    document.querySelectorAll('.filter-btn').forEach(btn => {
      btn.addEventListener('click', (e) => this.filterPlaylist(e.target.dataset.filter));
    });
  }

  renderPlaylist() {
    this.elements.playlist.innerHTML = '';
    
    this.playlist.forEach((track, index) => {
      const playlistItem = document.createElement('div');
      playlistItem.className = 'playlist-item';
      playlistItem.dataset.index = index;
      
      playlistItem.innerHTML = `
        <div class="track-number">${index + 1}</div>
        <img src="${track.artwork}" alt="${track.album}" class="track-artwork" onerror="this.src='/assets/music/default-album.jpg'">
        <div class="track-info">
          <div class="track-title">${track.title}</div>
          <div class="track-artist">${track.artist}</div>
        </div>
        <div class="track-duration">${track.duration}</div>
      `;
      
      playlistItem.addEventListener('click', () => this.playTrack(index));
      this.elements.playlist.appendChild(playlistItem);
    });
  }

  playTrack(index) {
    this.currentTrackIndex = index;
    const track = this.playlist[index];
    
    this.audio.src = track.audio;
    this.audio.load();
    
    this.updateDisplay();
    this.updatePlaylistUI();
    
    if (this.isPlaying) {
      this.audio.play().catch(e => console.log('Playback failed:', e));
    }
  }

  togglePlayPause() {
    if (this.isPlaying) {
      this.pause();
    } else {
      this.play();
    }
  }

  play() {
    this.audio.play().then(() => {
      this.isPlaying = true;
      this.elements.playPauseBtn.textContent = '⏸️';
    }).catch(e => {
      console.log('Playback failed:', e);
      // Show user-friendly message
      this.showMessage('Unable to play this track. Please check if the audio file is available.');
    });
  }

  pause() {
    this.audio.pause();
    this.isPlaying = false;
    this.elements.playPauseBtn.textContent = '▶️';
  }

  previousTrack() {
    if (this.currentTrackIndex > 0) {
      this.playTrack(this.currentTrackIndex - 1);
    }
  }

  nextTrack() {
    if (this.currentTrackIndex < this.playlist.length - 1) {
      this.playTrack(this.currentTrackIndex + 1);
    } else if (this.repeatMode === 'all') {
      this.playTrack(0);
    }
  }

  toggleShuffle() {
    this.isShuffled = !this.isShuffled;
    this.elements.shuffleBtn.style.opacity = this.isShuffled ? '1' : '0.5';
    
    if (this.isShuffled) {
      this.shufflePlaylist();
    } else {
      this.loadPlaylist(); // Reset to original order
      this.renderPlaylist();
    }
  }

  shufflePlaylist() {
    const shuffled = [...this.playlist];
    for (let i = shuffled.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1));
      [shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]];
    }
    this.playlist = shuffled;
    this.renderPlaylist();
  }

  toggleRepeat() {
    const modes = ['none', 'one', 'all'];
    const currentIndex = modes.indexOf(this.repeatMode);
    this.repeatMode = modes[(currentIndex + 1) % modes.length];
    
    const icons = ['🔁', '🔂', '🔁'];
    this.elements.repeatBtn.textContent = icons[currentIndex];
    this.elements.repeatBtn.style.opacity = this.repeatMode === 'none' ? '0.5' : '1';
  }

  toggleMute() {
    if (this.audio.muted) {
      this.audio.muted = false;
      this.elements.muteBtn.textContent = '🔊';
    } else {
      this.audio.muted = true;
      this.elements.muteBtn.textContent = '🔇';
    }
  }

  setVolume(volume) {
    this.volume = volume;
    this.audio.volume = volume;
    this.elements.volumeSlider.value = volume * 100;
  }

  seekTo(percentage) {
    if (this.audio.duration) {
      this.audio.currentTime = this.audio.duration * percentage;
    }
  }

  updateProgress() {
    if (this.audio.duration) {
      const percentage = (this.audio.currentTime / this.audio.duration) * 100;
      this.elements.progress.style.width = percentage + '%';
      
      this.elements.currentTime.textContent = this.formatTime(this.audio.currentTime);
    }
  }

  updateDisplay() {
    const track = this.playlist[this.currentTrackIndex];
    if (track) {
      this.elements.currentTitle.textContent = track.title;
      this.elements.currentArtist.textContent = track.artist;
      this.elements.currentAlbum.textContent = track.album;
      this.elements.currentArtwork.src = track.artwork;
      this.elements.currentArtwork.onerror = () => {
        this.elements.currentArtwork.src = '/assets/music/default-album.jpg';
      };
      
      if (this.audio.duration) {
        this.elements.totalTime.textContent = this.formatTime(this.audio.duration);
      }
    }
  }

  updatePlaylistUI() {
    document.querySelectorAll('.playlist-item').forEach((item, index) => {
      item.classList.toggle('playing', index === this.currentTrackIndex);
    });
  }

  handleTrackEnd() {
    if (this.repeatMode === 'one') {
      this.audio.currentTime = 0;
      this.audio.play();
    } else if (this.currentTrackIndex < this.playlist.length - 1) {
      this.nextTrack();
    } else if (this.repeatMode === 'all') {
      this.playTrack(0);
    }
  }

  filterPlaylist(filter) {
    // Update filter buttons
    document.querySelectorAll('.filter-btn').forEach(btn => {
      btn.classList.toggle('active', btn.dataset.filter === filter);
    });
    
    // Filter and re-render playlist
    let filteredPlaylist = this.playlist;
    if (filter !== 'all') {
      filteredPlaylist = this.playlist.filter(track => track.genre === filter);
    }
    
    // Re-render with filtered results
    this.elements.playlist.innerHTML = '';
    filteredPlaylist.forEach((track, index) => {
      const originalIndex = this.playlist.indexOf(track);
      const playlistItem = document.createElement('div');
      playlistItem.className = 'playlist-item';
      playlistItem.dataset.index = originalIndex;
      
      playlistItem.innerHTML = `
        <div class="track-number">${index + 1}</div>
        <img src="${track.artwork}" alt="${track.album}" class="track-artwork" onerror="this.src='/assets/music/default-album.jpg'">
        <div class="track-info">
          <div class="track-title">${track.title}</div>
          <div class="track-artist">${track.artist}</div>
        </div>
        <div class="track-duration">${track.duration}</div>
      `;
      
      playlistItem.addEventListener('click', () => this.playTrack(originalIndex));
      this.elements.playlist.appendChild(playlistItem);
    });
  }

  formatTime(seconds) {
    const mins = Math.floor(seconds / 60);
    const secs = Math.floor(seconds % 60);
    return `${mins}:${secs.toString().padStart(2, '0')}`;
  }

  showMessage(message) {
    // Simple message display - you could enhance this with a proper notification system
    const messageDiv = document.createElement('div');
    messageDiv.style.cssText = `
      position: fixed;
      top: 20px;
      right: 20px;
      background: #ff6b6b;
      color: white;
      padding: 15px 20px;
      border-radius: 8px;
      z-index: 1000;
      box-shadow: 0 4px 15px rgba(0,0,0,0.2);
    `;
    messageDiv.textContent = message;
    document.body.appendChild(messageDiv);
    
    setTimeout(() => {
      document.body.removeChild(messageDiv);
    }, 3000);
  }
}

// Initialize the music player when the page loads
document.addEventListener('DOMContentLoaded', () => {
  new MusicPlayer();
});
</script>
