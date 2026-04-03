<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>HELLO WORLD - JWX Fighter</title>
<style>
* { margin: 0; padding: 0; box-sizing: border-box; }
html, body { width: 100%; height: 100%; overflow: hidden; background: #000; display: flex; align-items: center; justify-content: center; }
canvas { image-rendering: pixelated; image-rendering: crisp-edges; display: block; }
</style>
</head>
<body>
<canvas id="gameCanvas" width="480" height="270"></canvas>
<script>
'use strict';

// ═══════════════════════════════════════════
// SECTION 1: CONSTANTS & ENUMS
// ═══════════════════════════════════════════

const CANVAS_W = 480;
const CANVAS_H = 270;
const STAGE_WIDTH = 960;

const PHYSICS = Object.freeze({
  GRAVITY: 1800,
  JUMP_VELOCITY: -620,
  MAX_FALL_SPEED: 900,
  WALK_SPEED: 160,
  DASH_SPEED: 380,
  DASH_DURATION: 0.18,
  KNOCKBACK_VELOCITY: 280,
  GROUND_Y: 210,
  LEFT_BOUNDARY: 30,
  RIGHT_BOUNDARY: 930,
  PUSH_DISTANCE: 48,
});

// Fighter states
const FS = Object.freeze({
  IDLE: 'IDLE', WALKING: 'WALKING', JUMPING: 'JUMPING',
  CROUCHING: 'CROUCHING',
  ATK_LP: 'ATK_LP', ATK_HP: 'ATK_HP',
  ATK_LK: 'ATK_LK', ATK_HK: 'ATK_HK',
  ATK_CROUCH_LP: 'ATK_CROUCH_LP', ATK_CROUCH_HK: 'ATK_CROUCH_HK',
  ATK_AIR_LP: 'ATK_AIR_LP', ATK_AIR_HK: 'ATK_AIR_HK',
  ATK_SPECIAL: 'ATK_SPECIAL', ATK_SUPER: 'ATK_SUPER',
  BLOCKING: 'BLOCKING', CROUCH_BLOCKING: 'CROUCH_BLOCKING',
  HIT_STUN: 'HIT_STUN', KNOCKDOWN: 'KNOCKDOWN', RISING: 'RISING',
  THROW: 'THROW', THROWN: 'THROWN',
  DASHING: 'DASHING',
});

// Game states
const GS = Object.freeze({
  TITLE_SCREEN: 'TITLE_SCREEN',
  CHARACTER_SELECT: 'CHARACTER_SELECT',
  VS_SCREEN: 'VS_SCREEN',
  ROUND_INTRO: 'ROUND_INTRO',
  FIGHTING: 'FIGHTING',
  ROUND_END: 'ROUND_END',
  MATCH_END: 'MATCH_END',
  NEXT_OPPONENT: 'NEXT_OPPONENT',
  BOSS_INTRO: 'BOSS_INTRO',
  GAME_OVER: 'GAME_OVER',
  ENDING: 'ENDING',
});

// Frame data for normal moves: { startup, active, recovery, damage, stun, knockbackX, knockbackY, type }
const FRAME_DATA = Object.freeze({
  [FS.ATK_LP]:        { startup: 4,  active: 3, recovery: 8,  damage: 5,  stun: 10, knockbackX: 30,  knockbackY: 0,    type: 'punch',  hitboxW: 24, hitboxH: 16, hitboxX: 20, hitboxY: -24 },
  [FS.ATK_HP]:        { startup: 8,  active: 4, recovery: 18, damage: 12, stun: 20, knockbackX: 80,  knockbackY: -40,  type: 'punch',  hitboxW: 30, hitboxH: 20, hitboxX: 22, hitboxY: -28 },
  [FS.ATK_LK]:        { startup: 5,  active: 3, recovery: 10, damage: 6,  stun: 12, knockbackX: 30,  knockbackY: 0,    type: 'kick',   hitboxW: 28, hitboxH: 14, hitboxX: 18, hitboxY: -10 },
  [FS.ATK_HK]:        { startup: 10, active: 5, recovery: 22, damage: 15, stun: 25, knockbackX: 80,  knockbackY: -60,  type: 'kick',   hitboxW: 32, hitboxH: 18, hitboxX: 20, hitboxY: -14 },
  [FS.ATK_CROUCH_LP]: { startup: 4,  active: 2, recovery: 8,  damage: 4,  stun: 8,  knockbackX: 20,  knockbackY: 0,    type: 'punch',  hitboxW: 22, hitboxH: 14, hitboxX: 18, hitboxY: -8 },
  [FS.ATK_CROUCH_HK]: { startup: 12, active: 6, recovery: 28, damage: 14, stun: 0,  knockbackX: 60,  knockbackY: 0,    type: 'kick',   hitboxW: 36, hitboxH: 12, hitboxX: 16, hitboxY: 0, knockdown: true },
  [FS.ATK_AIR_LP]:    { startup: 5,  active: 4, recovery: 0,  damage: 7,  stun: 12, knockbackX: 30,  knockbackY: 20,   type: 'punch',  hitboxW: 24, hitboxH: 18, hitboxX: 16, hitboxY: -10 },
  [FS.ATK_AIR_HK]:    { startup: 7,  active: 5, recovery: 0,  damage: 16, stun: 0,  knockbackX: 60,  knockbackY: 40,   type: 'kick',   hitboxW: 30, hitboxH: 20, hitboxX: 18, hitboxY: -6, knockdown: true },
  [FS.ATK_SPECIAL]:   { startup: 6,  active: 8, recovery: 16, damage: 18, stun: 20, knockbackX: 120, knockbackY: -100, type: 'special', hitboxW: 28, hitboxH: 24, hitboxX: 20, hitboxY: -30 },
  [FS.ATK_SUPER]:     { startup: 10, active: 12, recovery: 20, damage: 30, stun: 30, knockbackX: 200, knockbackY: -80, type: 'special', hitboxW: 40, hitboxH: 30, hitboxX: 24, hitboxY: -34 },
  [FS.THROW]:         { startup: 5,  active: 1, recovery: 20, damage: 20, stun: 35, knockbackX: 150, knockbackY: -50, type: 'throw',   hitboxW: 20, hitboxH: 40, hitboxX: 16, hitboxY: -30, range: 32 },
});

// Special move types
const SPECIAL = Object.freeze({
  FIREBALL: 'FIREBALL',
  DP: 'DP',
  SPIN_KICK: 'SPIN_KICK',
  SUPER: 'SUPER',
});

// Character indices
const CHAR = Object.freeze({
  JWX: 0, JW_PLAYER: 1, CONNATIX: 2, VUALTO: 3,
  INPLAYER: 4, AUGXLABS: 5, QUANTUM_PATH: 6, HELLO: 7,
});

// Fight order (opponent char indices, before player removal)
const GAUNTLET_ORDER = [CHAR.JW_PLAYER, CHAR.CONNATIX, CHAR.VUALTO, CHAR.INPLAYER, CHAR.AUGXLABS, CHAR.QUANTUM_PATH];

// Difficulty scaling per fight
const DIFFICULTY = [
  { thinkMin: 14, thinkMax: 18, aggression: 0.40, blockRate: 0.15 },
  { thinkMin: 12, thinkMax: 18, aggression: 0.50, blockRate: 0.20 },
  { thinkMin: 10, thinkMax: 16, aggression: 0.55, blockRate: 0.25 },
  { thinkMin: 10, thinkMax: 14, aggression: 0.60, blockRate: 0.35 },
  { thinkMin: 8,  thinkMax: 14, aggression: 0.65, blockRate: 0.25 },
  { thinkMin: 7,  thinkMax: 12, aggression: 0.70, blockRate: 0.30 },
  { thinkMin: 6,  thinkMax: 12, aggression: 0.75, blockRate: 0.30 },
  { thinkMin: 6,  thinkMax: 10, aggression: 0.85, blockRate: 0.40 },
];

// Character definitions
const CHARACTERS = [
  { id: 'JWX', name: 'JWX', colors: { body: '#000000', text: '#FFFFFF', accent: '#FF4B00', limbs: '#2A2A2A', joints: '#FF4B00' }, stats: { hp: 100, speed: 1.0, attack: 1.0, special: 1.0 }, stars: { hp: 3, spd: 3, atk: 3, spc: 3 }, projectileColor: '#FF4B00', projectileShape: 'disc', aiProfile: { dashBias: 0, fireballBias: 0, throwBias: 0, blockBias: 0, aggressionBias: 0 }, superMove: { name: 'Stream Dominator', type: 'multi_projectile', count: 3, damageEach: 10 } },
  { id: 'JW_PLAYER', name: 'JW Player', colors: { body: '#FF1654', text: '#FFFFFF', accent: '#FF4500', limbs: '#CC3A00', joints: '#FF4500' }, stats: { hp: 100, speed: 1.4, attack: 1.0, special: 0.8 }, stars: { hp: 2, spd: 5, atk: 3, spc: 2 }, projectileColor: '#FF4500', projectileShape: 'bolt', aiProfile: { dashBias: 0.20, fireballBias: -0.15, throwBias: 0, blockBias: 0, aggressionBias: 0.15 }, superMove: { name: 'Broadcast Rush', type: 'teleport_combo', hits: 5, damageEach: 8 } },
  { id: 'CONNATIX', name: 'Connatix', colors: { body: '#1B2838', text: '#FFFFFF', accent: '#6C3BFF', limbs: '#5A2FCC', joints: '#FFFFFF' }, stats: { hp: 100, speed: 1.0, attack: 0.8, special: 1.4 }, stars: { hp: 2, spd: 3, atk: 2, spc: 5 }, projectileColor: '#6C3BFF', projectileShape: 'arc', aiProfile: { dashBias: 0, fireballBias: 0.30, throwBias: 0, blockBias: 0, aggressionBias: -0.20 }, superMove: { name: 'Ad Barrage', type: 'projectile_rain', count: 8, damageEach: 6 } },
  { id: 'VUALTO', name: 'VUALTO', colors: { body: '#00B4D8', text: '#FFFFFF', accent: '#0077A8', limbs: '#008BA3', joints: '#00B4D8' }, stats: { hp: 100, speed: 0.8, attack: 1.2, special: 1.0 }, stars: { hp: 5, spd: 2, atk: 4, spc: 3 }, projectileColor: '#00B4D8', projectileShape: 'ring', aiProfile: { dashBias: 0, fireballBias: -0.20, throwBias: 0.25, blockBias: 0, aggressionBias: 0.15 }, superMove: { name: 'Stream Lock', type: 'grab_super', damage: 45 } },
  { id: 'INPLAYER', name: 'InPlayer', colors: { body: '#E63946', text: '#FFFFFF', accent: '#9B1D24', limbs: '#CC2233', joints: '#E63946' }, stats: { hp: 100, speed: 1.0, attack: 1.0, special: 1.2 }, stars: { hp: 4, spd: 3, atk: 3, spc: 4 }, projectileColor: '#E63946', projectileShape: 'shield', aiProfile: { dashBias: 0, fireballBias: 0, throwBias: 0, blockBias: 0.20, aggressionBias: -0.15 }, superMove: { name: 'Paywall', type: 'barrier', duration: 300 } },
  { id: 'AUGXLABS', name: 'Aug X Labs', colors: { body: '#000000', text: '#9B59F0', accent: '#FFD700', limbs: '#C4A000', joints: '#FF6B00' }, stats: { hp: 100, speed: 1.4, attack: 1.2, special: 1.0 }, stars: { hp: 2, spd: 5, atk: 4, spc: 3 }, projectileColor: '#FFD700', projectileShape: 'lightning', aiProfile: { dashBias: 0, fireballBias: 0, throwBias: 0, blockBias: 0, aggressionBias: 0, wildCard: true }, superMove: { name: 'Augmented Fury', type: 'power_up', duration: 480, damageMult: 1.5 } },
  { id: 'QUANTUM_PATH', name: 'Quantum Path', colors: { body: '#001A0D', text: '#00FF88', accent: '#00CC66', limbs: '#003322', joints: '#00FF88' }, stats: { hp: 100, speed: 1.2, attack: 1.0, special: 1.2 }, stars: { hp: 3, spd: 4, atk: 3, spc: 4 }, projectileColor: '#00FF88', projectileShape: 'sphere', aiProfile: { dashBias: 0, fireballBias: 0, throwBias: 0, blockBias: 0, aggressionBias: 0, parryBias: 0.10, specialCancelBias: 0.15 }, superMove: { name: 'Quantum Leap', type: 'invisible', duration: 180 } },
  { id: 'HELLO', name: 'HELLO', colors: { body: '#1A6EBD', text: '#FFFFFF', accent: '#87CEEB', limbs: '#333333', joints: '#555555', land: '#2D8A4E' }, stats: { hp: 300, speed: 1.0, attack: 1.4, special: 1.4 }, stars: { hp: 6, spd: 3, atk: 5, spc: 5 }, projectileColor: '#87CEEB', projectileShape: 'wave', aiProfile: {}, superMove: { name: 'World Spin', type: 'boss_spin', damagePerHit: 8 } },
];

// Stage definitions
const STAGES = [
  { id: 'broadcast',   name: 'The Broadcast Stage',  floorColor: '#1A1000', bgColor: '#0D1B2A', accentColor: '#FF4500' },
  { id: 'ad_alley',    name: 'The Ad Network Alley',  floorColor: '#2A2A2A', bgColor: '#1A0030', accentColor: '#6C3BFF' },
  { id: 'stream_vault', name: 'The Stream Vault',      floorColor: '#1A2030', bgColor: '#2A3240', accentColor: '#00B4D8' },
  { id: 'paywall',     name: 'The Paywall Plaza',     floorColor: '#3A1020', bgColor: '#4A0010', accentColor: '#FFD700' },
  { id: 'ai_lab',      name: 'The AI Lab',            floorColor: '#E0E0E0', bgColor: '#F0F0F0', accentColor: '#FFD700' },
  { id: 'data_grid',   name: 'The Data Grid',         floorColor: '#000000', bgColor: '#000000', accentColor: '#00FF44' },
  { id: 'mirror',      name: 'Mirror Stage',          floorColor: '#A0A0A0', bgColor: '#C0C0C0', accentColor: '#FFFFFF' },
  { id: 'globe_arena', name: 'The Globe Arena',       floorColor: '#303030', bgColor: '#000010', accentColor: '#00FFCC' },
];


// ═══════════════════════════════════════════
// SECTION 2: AUDIO ENGINE
// ═══════════════════════════════════════════

let audioCtx = null;
let masterGain, musicGain, sfxGain;
let audioInitialized = false;
let musicScheduler = null;
let pitchMultiplier = 1.0;

function initAudio() {
  if (audioInitialized) return;
  audioCtx = new (window.AudioContext || window.webkitAudioContext)();
  masterGain = audioCtx.createGain();
  masterGain.gain.value = 0.6;
  masterGain.connect(audioCtx.destination);
  musicGain = audioCtx.createGain();
  musicGain.gain.value = 0.4;
  musicGain.connect(masterGain);
  sfxGain = audioCtx.createGain();
  sfxGain.gain.value = 0.8;
  sfxGain.connect(masterGain);
  audioInitialized = true;
}

// Note frequencies
const N = {
  C3:130.81,D3:146.83,Eb3:155.56,E3:164.81,F3:174.61,Fs3:185.00,G3:196.00,Ab3:207.65,A3:220.00,Bb3:233.08,B3:246.94,
  C4:261.63,D4:293.66,Eb4:311.13,E4:329.63,F4:349.23,Fs4:369.99,G4:392.00,Ab4:415.30,A4:440.00,Bb4:466.16,B4:493.88,
  C5:523.25,D5:587.33,Eb5:622.25,E5:659.26,F5:698.46,Fs5:739.99,G5:783.99,Ab5:830.61,A5:880.00,Bb5:932.33,B5:987.77,
  C6:1046.50,R:0
};

function scheduleNote(freq, startTime, duration, wave) {
  if (!audioCtx || audioCtx.state !== 'running' || freq <= 0) return;
  const osc = audioCtx.createOscillator();
  const gain = audioCtx.createGain();
  osc.type = wave || 'square';
  osc.frequency.value = freq * pitchMultiplier;
  gain.gain.setValueAtTime(0.25, startTime);
  gain.gain.exponentialRampToValueAtTime(0.001, startTime + duration - 0.01);
  osc.connect(gain);
  gain.connect(musicGain);
  osc.start(startTime);
  osc.stop(startTime + duration + 0.02);
}

function playTrack(trackDef, loop) {
  stopMusic();
  if (!audioCtx || audioCtx.state !== 'running' || !trackDef) return;
  if (loop === undefined) loop = true;
  const secPerBeat = 60 / trackDef.bpm;
  const voiceCursors = trackDef.voices.map(() => ({ idx: 0, time: audioCtx.currentTime + 0.05 }));
  function tick() {
    if (!audioCtx) return;
    const horizon = audioCtx.currentTime + 0.15;
    for (let v = 0; v < trackDef.voices.length; v++) {
      const voice = trackDef.voices[v];
      const cursor = voiceCursors[v];
      while (cursor.time < horizon) {
        const note = voice.notes[cursor.idx];
        const dur = note.d * secPerBeat;
        if (note.f > 0) scheduleNote(note.f, cursor.time, dur, voice.wave);
        cursor.time += dur;
        cursor.idx++;
        if (cursor.idx >= voice.notes.length) {
          if (loop) cursor.idx = 0;
          else break;
        }
      }
    }
  }
  musicScheduler = setInterval(tick, 25);
  tick();
}

function stopMusic(fadeDur) {
  if (musicScheduler) { clearInterval(musicScheduler); musicScheduler = null; }
  if (musicGain && audioCtx) {
    const now = audioCtx.currentTime;
    const fd = fadeDur || 0.01;
    musicGain.gain.setValueAtTime(musicGain.gain.value, now);
    musicGain.gain.linearRampToValueAtTime(0.001, now + fd);
    setTimeout(() => { if (musicGain) musicGain.gain.setValueAtTime(0.4, audioCtx.currentTime); }, (fd + 0.05) * 1000);
  }
}

function playSFX(freq, freqEnd, dur, wave, vol) {
  if (!audioCtx || audioCtx.state !== 'running') return;
  const now = audioCtx.currentTime;
  const osc = audioCtx.createOscillator();
  const gain = audioCtx.createGain();
  osc.type = wave || 'square';
  osc.frequency.setValueAtTime(freq, now);
  if (freqEnd && freqEnd !== freq) osc.frequency.exponentialRampToValueAtTime(Math.max(freqEnd, 20), now + dur);
  gain.gain.setValueAtTime(vol || 0.5, now);
  gain.gain.exponentialRampToValueAtTime(0.001, now + dur);
  osc.connect(gain);
  gain.connect(sfxGain);
  osc.start(now);
  osc.stop(now + dur + 0.02);
}

let noiseBuffer = null;
function ensureNoiseBuffer() {
  if (noiseBuffer || !audioCtx) return;
  const sr = audioCtx.sampleRate;
  const buf = audioCtx.createBuffer(1, sr * 2, sr);
  const data = buf.getChannelData(0);
  for (let i = 0; i < data.length; i++) data[i] = Math.random() * 2 - 1;
  noiseBuffer = buf;
}

function playNoiseBurst(duration, filterFreq) {
  if (!audioCtx || audioCtx.state !== 'running') return;
  ensureNoiseBuffer();
  const now = audioCtx.currentTime;
  const src = audioCtx.createBufferSource();
  src.buffer = noiseBuffer;
  const filter = audioCtx.createBiquadFilter();
  filter.type = 'lowpass';
  filter.frequency.value = filterFreq || 200;
  const gain = audioCtx.createGain();
  gain.gain.setValueAtTime(0.6, now);
  gain.gain.exponentialRampToValueAtTime(0.001, now + duration);
  src.connect(filter);
  filter.connect(gain);
  gain.connect(sfxGain);
  src.start(now);
  src.stop(now + duration + 0.05);
}

// SFX shortcuts
const SFX = {
  punchLight:      () => playSFX(280, 180, 0.08, 'square'),
  punchHeavy:      () => playSFX(180, 80, 0.14, 'square'),
  kickLight:       () => playSFX(320, 200, 0.09, 'sawtooth'),
  kickHeavy:       () => playSFX(200, 100, 0.16, 'sawtooth'),
  block:           () => playSFX(440, 440, 0.06, 'square'),
  whiff:           () => playSFX(600, 400, 0.05, 'sine'),
  jump:            () => playSFX(300, 500, 0.10, 'triangle'),
  land:            () => playSFX(150, 150, 0.04, 'square'),
  fireballLaunch:  () => playSFX(500, 300, 0.12, 'sawtooth'),
  fireballHit:     () => playSFX(350, 150, 0.10, 'square'),
  specialActivate: () => playSFX(200, 800, 0.20, 'sawtooth'),
  superActivate:   () => { playSFX(200, 200, 0.40, 'sawtooth', 0.3); playSFX(400, 400, 0.40, 'sawtooth', 0.3); playSFX(600, 600, 0.40, 'sawtooth', 0.3); },
  ko:              () => { playSFX(180, 80, 0.14, 'square'); playNoiseBurst(0.3, 200); },
  roundStart:      () => playSFX(660, 660, 0.08, 'square'),
  cursorMove:      () => playSFX(220, 220, 0.04, 'square'),
  cursorConfirm:   () => { playSFX(440, 440, 0.06, 'triangle'); setTimeout(() => playSFX(660, 660, 0.06, 'triangle'), 60); },
  cursorError:     () => playSFX(150, 150, 0.20, 'square'),
  timerLow:        () => playSFX(880, 880, 0.08, 'square'),
  helloTease:      () => playSFX(80, 40, 0.50, 'sine', 0.6),
  parry:           () => playSFX(880, 1200, 0.08, 'triangle'),
  throwHit:        () => playSFX(200, 100, 0.18, 'square'),
  comboHit:        (c) => playSFX(220 + (c||1) * 40, 220 + (c||1) * 40, 0.03, 'triangle'),
};

// ── Music Tracks ──

const TRACK_TITLE = { bpm: 80, voices: [
  { wave: 'square', notes: [
    {f:N.A4,d:1},{f:N.R,d:0.5},{f:N.E4,d:0.5},{f:N.C4,d:1},{f:N.R,d:1},
    {f:N.A4,d:0.5},{f:N.Ab4,d:0.5},{f:N.E4,d:1},{f:N.R,d:1},
    {f:N.A4,d:1},{f:N.R,d:0.5},{f:N.G4,d:0.5},{f:N.E4,d:1},{f:N.R,d:1},
    {f:N.F4,d:0.5},{f:N.E4,d:0.5},{f:N.C4,d:1.5},{f:N.R,d:0.5},
  ]},
  { wave: 'triangle', notes: [
    {f:N.A3,d:4},{f:N.E3,d:4},{f:N.A3,d:4},{f:N.F3,d:2},{f:N.E3,d:2},
  ]},
]};

const TRACK_SELECT = { bpm: 140, voices: [
  { wave: 'square', notes: [
    {f:N.C5,d:0.5},{f:N.E5,d:0.5},{f:N.G5,d:0.5},{f:N.E5,d:0.5},
    {f:N.C5,d:0.5},{f:N.D5,d:0.5},{f:N.E5,d:0.5},{f:N.R,d:0.5},
    {f:N.F5,d:0.5},{f:N.E5,d:0.5},{f:N.D5,d:0.5},{f:N.C5,d:0.5},
    {f:N.A4,d:0.5},{f:N.G4,d:0.5},{f:N.A4,d:0.5},{f:N.R,d:0.5},
  ]},
  { wave: 'triangle', notes: [
    {f:N.C3,d:0.5},{f:N.C3,d:0.5},{f:N.G3,d:0.5},{f:N.G3,d:0.5},
    {f:N.A3,d:0.5},{f:N.A3,d:0.5},{f:N.F3,d:0.5},{f:N.G3,d:0.5},
  ]},
  { wave: 'sawtooth', notes: [
    {f:N.C4,d:0.25},{f:N.R,d:0.75},{f:N.G4,d:0.25},{f:N.R,d:0.75},
    {f:N.A4,d:0.25},{f:N.R,d:0.75},{f:N.F4,d:0.25},{f:N.R,d:0.75},
  ]},
]};

const TRACK_STAGE1 = { bpm: 160, voices: [
  { wave: 'square', notes: [
    {f:N.A4,d:0.5},{f:N.R,d:0.25},{f:N.A4,d:0.25},{f:N.C5,d:0.5},{f:N.D5,d:0.5},
    {f:N.E5,d:0.5},{f:N.D5,d:0.25},{f:N.C5,d:0.25},{f:N.A4,d:0.5},{f:N.R,d:0.5},
    {f:N.G4,d:0.5},{f:N.A4,d:0.5},{f:N.C5,d:0.5},{f:N.A4,d:0.25},{f:N.G4,d:0.25},
    {f:N.E4,d:1},{f:N.R,d:0.5},
  ]},
  { wave: 'triangle', notes: [
    {f:N.A3,d:0.5},{f:N.A3,d:0.5},{f:N.C3,d:0.5},{f:N.C3,d:0.5},
    {f:N.D3,d:0.5},{f:N.D3,d:0.5},{f:N.E3,d:0.5},{f:N.E3,d:0.5},
    {f:N.F3,d:0.5},{f:N.F3,d:0.5},{f:N.G3,d:0.5},{f:N.G3,d:0.5},
    {f:N.A3,d:0.5},{f:N.E3,d:0.5},{f:N.A3,d:0.5},{f:N.A3,d:0.5},
  ]},
]};

const TRACK_STAGE2 = { bpm: 130, voices: [
  { wave: 'sawtooth', notes: [
    {f:N.E4,d:0.5},{f:N.G4,d:0.5},{f:N.A4,d:0.5},{f:N.Bb4,d:0.5},
    {f:N.A4,d:1},{f:N.G4,d:0.5},{f:N.E4,d:0.5},
    {f:N.D4,d:0.5},{f:N.E4,d:0.5},{f:N.G4,d:1},{f:N.R,d:1},
  ]},
  { wave: 'triangle', notes: [
    {f:N.E3,d:0.25},{f:N.R,d:0.25},{f:N.E3,d:0.25},{f:N.R,d:0.25},
    {f:N.G3,d:0.25},{f:N.R,d:0.25},{f:N.G3,d:0.25},{f:N.R,d:0.25},
    {f:N.A3,d:0.25},{f:N.R,d:0.25},{f:N.Bb3,d:0.25},{f:N.R,d:0.25},
    {f:N.A3,d:0.5},{f:N.G3,d:0.5},{f:N.E3,d:0.5},{f:N.D3,d:0.5},{f:N.E3,d:0.5},{f:N.R,d:0.5},
  ]},
]};

const TRACK_STAGE3 = { bpm: 150, voices: [
  { wave: 'square', notes: [
    {f:N.D4,d:0.25},{f:N.R,d:0.25},{f:N.D4,d:0.25},{f:N.R,d:0.25},
    {f:N.F4,d:0.25},{f:N.R,d:0.25},{f:N.A4,d:0.5},
    {f:N.G4,d:0.25},{f:N.R,d:0.25},{f:N.F4,d:0.25},{f:N.D4,d:0.25},
    {f:N.C4,d:0.5},{f:N.D4,d:0.5},{f:N.R,d:0.5},
  ]},
  { wave: 'triangle', notes: [
    {f:N.D3,d:0.5},{f:N.D3,d:0.5},{f:N.D3,d:0.5},{f:N.F3,d:0.5},
    {f:N.G3,d:0.5},{f:N.G3,d:0.5},{f:N.F3,d:0.5},{f:N.D3,d:0.5},
  ]},
]};

const TRACK_STAGE4 = { bpm: 120, voices: [
  { wave: 'square', notes: [
    {f:N.Bb4,d:1},{f:N.D5,d:0.5},{f:N.F5,d:0.5},
    {f:N.Bb5,d:1},{f:N.R,d:0.5},{f:N.F5,d:0.5},
    {f:N.D5,d:0.5},{f:N.Eb5,d:0.5},{f:N.F5,d:1},
    {f:N.Bb4,d:1},{f:N.R,d:1},
  ]},
  { wave: 'triangle', notes: [
    {f:N.Bb3,d:1},{f:N.Bb3,d:1},{f:N.F3,d:1},{f:N.F3,d:1},
    {f:N.Eb3,d:1},{f:N.F3,d:1},{f:N.Bb3,d:1},{f:N.Bb3,d:1},
  ]},
]};

const TRACK_STAGE5 = { bpm: 170, voices: [
  { wave: 'square', notes: [
    {f:N.Fs4,d:0.25},{f:N.A4,d:0.25},{f:N.Fs5,d:0.25},{f:N.E5,d:0.25},
    {f:N.D5,d:0.25},{f:N.Fs4,d:0.25},{f:N.A4,d:0.25},{f:N.B4,d:0.25},
    {f:N.Fs5,d:0.25},{f:N.E5,d:0.25},{f:N.D5,d:0.25},{f:N.B4,d:0.25},
    {f:N.A4,d:0.25},{f:N.Fs4,d:0.25},{f:N.R,d:0.5},
  ]},
  { wave: 'triangle', notes: [
    {f:N.Fs3,d:0.5},{f:N.Fs3,d:0.5},{f:N.D3,d:0.5},{f:N.D3,d:0.5},
    {f:N.B3,d:0.5},{f:N.A3,d:0.5},{f:N.Fs3,d:0.5},{f:N.Fs3,d:0.5},
  ]},
]};

const TRACK_STAGE6 = { bpm: 110, voices: [
  { wave: 'square', notes: [
    {f:N.B4,d:0.5},{f:N.R,d:1},{f:N.Fs4,d:0.25},{f:N.R,d:0.75},
    {f:N.B4,d:0.25},{f:N.R,d:0.25},{f:N.D5,d:0.5},{f:N.R,d:0.5},
    {f:N.A4,d:0.5},{f:N.R,d:1.5},{f:N.Fs4,d:0.5},{f:N.R,d:0.5},
  ]},
  { wave: 'triangle', notes: [
    {f:N.B3,d:2},{f:N.Fs3,d:2},{f:N.D3,d:2},{f:N.A3,d:2},
  ]},
]};

const TRACK_STAGE7 = { bpm: 90, voices: [
  { wave: 'square', notes: [
    {f:N.C4,d:1},{f:N.B3,d:1},{f:N.Bb3,d:0.5},{f:N.A3,d:0.5},{f:N.R,d:1},
    {f:N.Eb4,d:0.5},{f:N.D4,d:0.5},{f:N.Ab3,d:1},{f:N.R,d:1},
    {f:N.Fs4,d:0.5},{f:N.F4,d:0.5},{f:N.E4,d:1},{f:N.R,d:1},
  ]},
  { wave: 'triangle', notes: [
    {f:N.E3,d:2},{f:N.Bb3,d:2},{f:N.Fs3,d:2},{f:N.C3,d:2},
  ]},
]};

const TRACK_BOSS = { bpm: 180, voices: [
  { wave: 'square', notes: [
    {f:N.E5,d:0.5},{f:N.E5,d:0.25},{f:N.R,d:0.25},{f:N.G5,d:0.5},{f:N.A5,d:0.25},{f:N.G5,d:0.25},
    {f:N.E5,d:0.5},{f:N.D5,d:0.5},{f:N.C5,d:0.5},{f:N.B4,d:0.25},{f:N.C5,d:0.25},
    {f:N.E5,d:0.25},{f:N.F5,d:0.25},{f:N.G5,d:0.5},{f:N.A5,d:0.5},
    {f:N.B5,d:0.5},{f:N.A5,d:0.25},{f:N.G5,d:0.25},{f:N.E5,d:0.5},{f:N.R,d:0.25},{f:N.E5,d:0.25},
    {f:N.D5,d:0.5},{f:N.C5,d:0.5},{f:N.B4,d:1},
  ]},
  { wave: 'triangle', notes: [
    {f:N.E3,d:0.5},{f:N.E3,d:0.5},{f:N.E3,d:0.5},{f:N.G3,d:0.5},
    {f:N.A3,d:0.5},{f:N.A3,d:0.5},{f:N.G3,d:0.5},{f:N.E3,d:0.5},
    {f:N.C3,d:0.5},{f:N.C3,d:0.5},{f:N.D3,d:0.5},{f:N.D3,d:0.5},
    {f:N.E3,d:0.5},{f:N.E3,d:0.5},{f:N.B3,d:0.5},{f:N.E3,d:0.5},
  ]},
  { wave: 'sawtooth', notes: [
    {f:N.E4,d:0.25},{f:N.R,d:0.25},{f:N.E4,d:0.25},{f:N.R,d:0.25},
    {f:N.G4,d:0.25},{f:N.R,d:0.75},{f:N.A4,d:0.25},{f:N.R,d:0.25},
    {f:N.A4,d:0.25},{f:N.R,d:0.25},{f:N.G4,d:0.25},{f:N.R,d:0.75},
    {f:N.E4,d:0.25},{f:N.R,d:0.25},{f:N.D4,d:0.25},{f:N.R,d:0.25},
    {f:N.C4,d:0.25},{f:N.R,d:0.25},{f:N.B3,d:0.25},{f:N.R,d:0.75},
  ]},
]};

const TRACK_VICTORY = { bpm: 160, voices: [
  { wave: 'square', notes: [
    {f:N.C5,d:0.5},{f:N.E5,d:0.5},{f:N.G5,d:0.5},{f:N.C6,d:1.5},
    {f:N.R,d:0.5},{f:N.G5,d:0.5},{f:N.C6,d:2},
  ]},
  { wave: 'triangle', notes: [{f:N.C3,d:2},{f:N.G3,d:2},{f:N.C3,d:2}]},
]};

const TRACK_GAMEOVER = { bpm: 80, voices: [
  { wave: 'square', notes: [{f:N.E4,d:1},{f:N.Eb4,d:1},{f:N.C4,d:2}]},
  { wave: 'triangle', notes: [{f:N.A3,d:2},{f:N.Ab3,d:2}]},
]};

const TRACK_ENDING = { bpm: 100, voices: [
  { wave: 'square', notes: [
    {f:N.C4,d:2},{f:N.R,d:1},{f:N.E4,d:1},{f:N.G4,d:1},{f:N.R,d:0.5},
    {f:N.C5,d:1},{f:N.E5,d:1},{f:N.G5,d:1.5},{f:N.C6,d:3},{f:N.R,d:2},
  ]},
  { wave: 'triangle', notes: [
    {f:N.C3,d:4},{f:N.G3,d:4},{f:N.C3,d:2},{f:N.E3,d:2},{f:N.C3,d:4},
  ]},
]};

const STAGE_TRACKS = [TRACK_STAGE1, TRACK_STAGE2, TRACK_STAGE3, TRACK_STAGE4, TRACK_STAGE5, TRACK_STAGE6, TRACK_STAGE7, TRACK_BOSS];


// ═══════════════════════════════════════════
// SECTION 3: INPUT SYSTEM
// ═══════════════════════════════════════════

const keys = {};
const INPUT_BUFFER_SIZE = 16;
const inputBuffer = [];
let justPressed = {};

document.addEventListener('keydown', (e) => {
  if (!audioInitialized) { initAudio(); }
  if (audioCtx && audioCtx.state === 'suspended') audioCtx.resume();
  if (!keys[e.key]) justPressed[e.key] = true;
  keys[e.key] = true;
  e.preventDefault();
});
document.addEventListener('keyup', (e) => { keys[e.key] = false; e.preventDefault(); });

function sampleInput(frameCount) {
  const dirs = new Set();
  if (keys['ArrowLeft'] || keys['a'] || keys['A']) dirs.add('L');
  if (keys['ArrowRight'] || keys['d'] || keys['D']) dirs.add('R');
  if (keys['ArrowUp'] || keys['w'] || keys['W']) dirs.add('U');
  if (keys['ArrowDown'] || keys['s'] || keys['S']) dirs.add('D');
  const buttons = new Set();
  if (justPressed['u'] || justPressed['U']) buttons.add('LP');
  if (justPressed['i'] || justPressed['I']) buttons.add('HP');
  if (justPressed['j'] || justPressed['J']) buttons.add('LK');
  if (justPressed['k'] || justPressed['K']) buttons.add('HK');
  if (keys['o'] || keys['O'] || keys['l'] || keys['L']) buttons.add('BL');
  inputBuffer.push({ dirs, buttons, frame: frameCount });
  if (inputBuffer.length > INPUT_BUFFER_SIZE) inputBuffer.shift();
  justPressed = {};
}

function encodeDir(dirs) {
  const l = dirs.has('L'), r = dirs.has('R'), u = dirs.has('U'), d = dirs.has('D');
  if (d && r) return 'DR'; if (d && l) return 'DL';
  if (u && r) return 'UR'; if (u && l) return 'UL';
  if (d) return 'D'; if (u) return 'U'; if (l) return 'L'; if (r) return 'R';
  return 'N';
}

function flipDir(d) {
  return d.replace('L','_R_').replace('R','L').replace('_R_','R');
}

// Super lenient motions — absolute directions, both left and right versions
const MOTIONS = {
  // Fireball: Down then Right
  QCF:   [['D','DL','DR'],['R','DR','UR']],
  // Fireball mirrored: Down then Left
  QCF_L: [['D','DL','DR'],['L','DL','UL']],
  // Spin kick: Down then Left
  QCB:   [['D','DL','DR'],['L','DL','UL']],
  // Spin kick mirrored: Down then Right
  QCB_L: [['D','DL','DR'],['R','DR','UR']],
  // Uppercut: Right then Down
  DP:    [['R','DR','UR'],['D','DL','DR']],
  // Uppercut mirrored: Left then Down
  DP_L:  [['L','DL','UL'],['D','DL','DR']],
  // Super: Down then Right
  HCF:   [['D','DL','DR'],['R','DR','UR']],
  // Super mirrored: Down then Left
  HCF_L: [['D','DL','DR'],['L','DL','UL']],
  // Dash — these still use facing via checkDash
  DASH_F: [['R'],['N','R'],['R']],
  DASH_B: [['L'],['N','L'],['L']],
};

function checkMotion(motionSeq) {
  // No facing flip — motions are absolute directions
  let seqIdx = 0;
  for (let i = 0; i < inputBuffer.length; i++) {
    const code = encodeDir(inputBuffer[i].dirs);
    if (motionSeq[seqIdx].includes(code)) {
      seqIdx++;
      if (seqIdx >= motionSeq.length) return true;
    }
  }
  return false;
}

function detectSpecialMove() {
  if (inputBuffer.length === 0) return null;
  // Very lenient: check if a button was pressed in the last 10 frames
  let hasPunch = false, hasHP = false, hasKick = false;
  const lookback = Math.min(10, inputBuffer.length);
  for (let i = inputBuffer.length - lookback; i < inputBuffer.length; i++) {
    const b = inputBuffer[i].buttons;
    if (b.has('LP') || b.has('HP')) hasPunch = true;
    if (b.has('HP')) hasHP = true;
    if (b.has('LK') || b.has('HK')) hasKick = true;
  }
  if (!hasPunch && !hasKick) return null;
  // Check both left and right versions of each motion
  if (hasHP && (checkMotion(MOTIONS.HCF) || checkMotion(MOTIONS.HCF_L))) return SPECIAL.SUPER;
  if (hasPunch && (checkMotion(MOTIONS.DP) || checkMotion(MOTIONS.DP_L))) return SPECIAL.DP;
  if (hasPunch && (checkMotion(MOTIONS.QCF) || checkMotion(MOTIONS.QCF_L))) return SPECIAL.FIREBALL;
  if (hasKick && (checkMotion(MOTIONS.QCB) || checkMotion(MOTIONS.QCB_L))) return SPECIAL.SPIN_KICK;
  return null;
}

function checkDash() {
  if (checkMotion(MOTIONS.DASH_F)) return 1;
  if (checkMotion(MOTIONS.DASH_B)) return -1;
  return 0;
}


// ═══════════════════════════════════════════
// SECTION 4: UTILITY FUNCTIONS
// ═══════════════════════════════════════════

function roundRect(ctx, x, y, w, h, r) {
  ctx.beginPath();
  ctx.moveTo(x + r, y);
  ctx.lineTo(x + w - r, y);
  ctx.quadraticCurveTo(x + w, y, x + w, y + r);
  ctx.lineTo(x + w, y + h - r);
  ctx.quadraticCurveTo(x + w, y + h, x + w - r, y + h);
  ctx.lineTo(x + r, y + h);
  ctx.quadraticCurveTo(x, y + h, x, y + h - r);
  ctx.lineTo(x, y + r);
  ctx.quadraticCurveTo(x, y, x + r, y);
  ctx.closePath();
}

function lerp(a, b, t) { return a + (b - a) * t; }
function clamp(v, min, max) { return Math.max(min, Math.min(max, v)); }

function aabbOverlap(a, b) {
  return a.x < b.x + b.w && a.x + a.w > b.x && a.y < b.y + b.h && a.y + a.h > b.y;
}

// Screen shake
let shakeX = 0, shakeY = 0, shakeFrames = 0, shakeMag = 0;
function triggerShake(magnitude, frames) { shakeMag = magnitude; shakeFrames = frames; }
function updateShake() {
  if (shakeFrames > 0) {
    shakeX = (Math.random() - 0.5) * shakeMag * 2;
    shakeY = (Math.random() - 0.5) * shakeMag * 2;
    shakeFrames--;
  } else { shakeX = 0; shakeY = 0; }
}


// ═══════════════════════════════════════════
// SECTION 5: PARTICLE SYSTEM
// ═══════════════════════════════════════════

const particles = [];
const MAX_PARTICLES = 200;

function spawnParticle(x, y, vx, vy, life, size, color) {
  if (particles.length >= MAX_PARTICLES) return;
  particles.push({ x, y, vx, vy, life, maxLife: life, size, color });
}

function spawnBurst(x, y, count, speed, life, size, color) {
  for (let i = 0; i < count; i++) {
    const angle = Math.random() * Math.PI * 2;
    const spd = speed * (0.5 + Math.random() * 0.5);
    spawnParticle(x, y, Math.cos(angle) * spd, Math.sin(angle) * spd, life, size, color);
  }
}

function updateParticles(dt) {
  for (let i = particles.length - 1; i >= 0; i--) {
    const p = particles[i];
    p.vy += PHYSICS.GRAVITY * 0.3 * dt;
    p.x += p.vx * dt;
    p.y += p.vy * dt;
    p.life -= dt;
    if (p.life <= 0) particles.splice(i, 1);
  }
}

function renderParticles(ctx, camX) {
  for (const p of particles) {
    const alpha = clamp(p.life / p.maxLife, 0, 1);
    ctx.globalAlpha = alpha;
    ctx.fillStyle = p.color;
    ctx.fillRect(p.x - camX - p.size / 2, p.y - p.size / 2, p.size, p.size);
  }
  ctx.globalAlpha = 1;
}


// ═══════════════════════════════════════════
// SECTION 6: PROJECTILE CLASS
// ═══════════════════════════════════════════

const projectiles = [];

class Projectile {
  constructor(owner, x, y, vx, vy, damage, color, shape, width, height) {
    this.owner = owner;
    this.x = x; this.y = y;
    this.vx = vx; this.vy = vy;
    this.damage = damage;
    this.color = color;
    this.shape = shape;
    this.w = width || 16; this.h = height || 12;
    this.dead = false;
    this.hasHit = false;
    this.life = 3;
    this.frame = 0;
  }
  update(dt) {
    this.x += this.vx * dt;
    this.y += this.vy * dt;
    this.life -= dt;
    this.frame++;
    if (this.life <= 0 || this.x < 0 || this.x > STAGE_WIDTH) this.dead = true;
  }
  getHitbox() {
    return { x: this.x - this.w / 2, y: this.y - this.h / 2, w: this.w, h: this.h };
  }
  draw(ctx, camX) {
    const sx = this.x - camX;
    const sy = this.y;
    ctx.fillStyle = this.color;
    const pulse = Math.sin(this.frame * 0.3) * 2;
    if (this.shape === 'disc') {
      ctx.beginPath(); ctx.arc(sx, sy, 6 + pulse, 0, Math.PI * 2); ctx.fill();
    } else if (this.shape === 'bolt') {
      ctx.fillRect(sx - 8, sy - 3, 16, 6);
      ctx.fillStyle = '#FFF';
      ctx.fillRect(sx - 6, sy - 1, 12, 2);
    } else if (this.shape === 'arc') {
      ctx.beginPath(); ctx.arc(sx, sy, 8 + pulse, -0.5, 0.5); ctx.lineWidth = 3; ctx.strokeStyle = this.color; ctx.stroke();
    } else if (this.shape === 'ring') {
      ctx.beginPath(); ctx.arc(sx, sy, 10 + pulse, 0, Math.PI * 2); ctx.lineWidth = 2; ctx.strokeStyle = this.color; ctx.stroke();
    } else if (this.shape === 'shield') {
      ctx.beginPath(); ctx.moveTo(sx, sy - 8); ctx.lineTo(sx + 7, sy - 4); ctx.lineTo(sx + 7, sy + 4); ctx.lineTo(sx, sy + 8); ctx.lineTo(sx - 7, sy + 4); ctx.lineTo(sx - 7, sy - 4); ctx.closePath(); ctx.fill();
    } else if (this.shape === 'lightning') {
      ctx.strokeStyle = this.color; ctx.lineWidth = 2; ctx.beginPath();
      ctx.moveTo(sx - 6, sy - 6); ctx.lineTo(sx + 2, sy - 1); ctx.lineTo(sx - 2, sy + 1); ctx.lineTo(sx + 6, sy + 6); ctx.stroke();
    } else if (this.shape === 'sphere') {
      ctx.beginPath(); ctx.arc(sx, sy, 7, 0, Math.PI * 2); ctx.fill();
      ctx.fillStyle = 'rgba(255,255,255,0.4)'; ctx.beginPath(); ctx.arc(sx - 2, sy - 2, 3, 0, Math.PI * 2); ctx.fill();
    } else if (this.shape === 'wave') {
      ctx.fillRect(sx - 16, sy - 8, 32, 16);
      ctx.fillStyle = 'rgba(255,255,255,0.3)'; ctx.fillRect(sx - 14, sy - 6, 28, 12);
    } else {
      ctx.beginPath(); ctx.arc(sx, sy, 6, 0, Math.PI * 2); ctx.fill();
    }
  }
}


// ═══════════════════════════════════════════
// SECTION 7: CHARACTER SPRITE RENDERERS
// ═══════════════════════════════════════════

function getAnimOffsets(state, frameCount) {
  const t = frameCount / 60;
  let bodyY = 0, armLY = 0, armRY = 0, legLY = 0, legRY = 0, armLX = 0, armRX = 0;
  switch (state) {
    case FS.IDLE:
      bodyY = Math.sin(t * 3) * 2;
      armLY = Math.sin(t * 2.5) * 3; armRY = Math.sin(t * 2.5 + Math.PI) * 3;
      legLY = Math.cos(t * 2) * 2; legRY = Math.cos(t * 2 + Math.PI) * 2;
      break;
    case FS.WALKING:
      bodyY = Math.sin(t * 8) * 1;
      armLY = Math.sin(t * 6) * 5; armRY = Math.sin(t * 6 + Math.PI) * 5;
      legLY = Math.sin(t * 6) * 6; legRY = Math.sin(t * 6 + Math.PI) * 6;
      break;
    case FS.JUMPING:
      armLY = -6; armRY = -6; legLY = 4; legRY = 4; armLX = -4; armRX = 4;
      break;
    case FS.CROUCHING: case FS.CROUCH_BLOCKING:
      bodyY = 8; armLY = 4; armRY = 4; legLY = 6; legRY = 6;
      break;
    case FS.ATK_LP: case FS.ATK_CROUCH_LP: case FS.ATK_AIR_LP:
      armRX = 18; armRY = -4;
      break;
    case FS.ATK_HP:
      armRX = 26; armRY = -6; bodyY = -2;
      break;
    case FS.ATK_LK:
      armLX = -4; armRX = -4; legRY = -4;
      break;
    case FS.ATK_HK: case FS.ATK_CROUCH_HK:
      armLX = -4; armRX = -4; legRY = -6;
      break;
    case FS.ATK_SPECIAL: case FS.ATK_SUPER:
      armLX = -8; armRX = 20; armLY = -4; armRY = -8; bodyY = -2;
      break;
    case FS.HIT_STUN:
      bodyY = 2; armLY = 4; armRY = 4; armLX = -6; armRX = -6; legLY = 2; legRY = 2;
      break;
    case FS.BLOCKING:
      bodyY = -1; armLY = -8; armRY = -4; armRX = 8; legLY = 2; legRY = 2;
      break;
    case FS.KNOCKDOWN:
      bodyY = 12; armLY = 8; armRY = 8; armLX = -8; armRX = 8; legLY = 8; legRY = 8;
      break;
    case FS.RISING:
      bodyY = 6; armLY = 4; armRY = 4; legLY = 4; legRY = 4;
      break;
    case FS.DASHING:
      bodyY = -1; armLY = -2; armRY = -2; armLX = -6; armRX = -6;
      break;
    case FS.THROW:
      armRX = 22; armRY = -2;
      break;
    case FS.THROWN:
      bodyY = 4; armLY = 6; armRY = 6; legLY = 4; legRY = 4;
      break;
  }
  return { bodyY, armLY, armRY, legLY, legRY, armLX, armRX };
}

// Body renderers
function drawJWXBody(ctx, cx, by, bw, bh, fc, st) {
  ctx.fillStyle = '#000000';
  roundRect(ctx, cx - bw/2, by, bw, bh, 4); ctx.fill();
  ctx.strokeStyle = '#FF4B00'; ctx.lineWidth = 1.5;
  roundRect(ctx, cx - bw/2 + 1, by + 1, bw - 2, bh - 2, 3); ctx.stroke();
  // Simplified jw cursive
  ctx.strokeStyle = '#E8003F'; ctx.lineWidth = 2.5; ctx.lineCap = 'round';
  const x = cx - bw/2;
  ctx.beginPath();
  ctx.moveTo(x + 6, by + 8); ctx.quadraticCurveTo(x + 6, by + 28, x + 10, by + 24);
  ctx.lineTo(x + 13, by + 10); ctx.lineTo(x + 17, by + 24); ctx.lineTo(x + 21, by + 10); ctx.lineTo(x + 25, by + 24);
  ctx.stroke();
  // X circle
  const ccx = x + 33, ccy = by + bh/2;
  ctx.fillStyle = '#1A1A1A'; ctx.beginPath(); ctx.arc(ccx, ccy, 8, 0, Math.PI*2); ctx.fill();
  ctx.strokeStyle = '#FFF'; ctx.lineWidth = 2;
  ctx.beginPath(); ctx.moveTo(ccx-5,ccy-5); ctx.lineTo(ccx+5,ccy+5); ctx.moveTo(ccx+5,ccy-5); ctx.lineTo(ccx-5,ccy+5); ctx.stroke();
  if (st === FS.ATK_SPECIAL || st === FS.ATK_SUPER) {
    ctx.fillStyle = 'rgba(255,75,0,0.3)'; roundRect(ctx, cx-bw/2, by, bw, bh, 4); ctx.fill();
  }
}

function drawJWPlayerBody(ctx, cx, by, bw, bh, fc, st) {
  ctx.fillStyle = '#FF1654'; roundRect(ctx, cx-bw/2, by, bw, bh, 8); ctx.fill();
  ctx.strokeStyle = '#1A1A1A'; ctx.lineWidth = 1; roundRect(ctx, cx-bw/2, by, bw, bh, 8); ctx.stroke();
  // Wavy W
  ctx.strokeStyle = '#FFFFFF'; ctx.lineWidth = 3; ctx.lineCap = 'round'; ctx.lineJoin = 'round';
  const sy = by + bh/2, sx = cx - bw/2 + 5;
  ctx.beginPath(); ctx.moveTo(sx, sy - 4);
  ctx.quadraticCurveTo(sx + 4, sy - 12, sx + 7, sy);
  ctx.quadraticCurveTo(sx + 10, sy + 10, sx + 14, sy);
  ctx.quadraticCurveTo(sx + 17, sy - 14, sx + 20, sy);
  ctx.quadraticCurveTo(sx + 23, sy + 8, sx + 26, sy - 2);
  ctx.quadraticCurveTo(sx + 28, sy - 8, sx + 30, sy - 6);
  ctx.stroke();
  if (st === FS.HIT_STUN) {
    const p = Math.sin(fc * 0.5) * 0.3 + 0.5;
    ctx.fillStyle = `rgba(255,255,255,${p * 0.3})`; roundRect(ctx, cx-bw/2, by, bw, bh, 8); ctx.fill();
  }
}

function drawConnatixBody(ctx, cx, by, bw, bh, fc, st) {
  const ccx = cx, ccy = by + bh/2, r = Math.min(bw, bh)/2 - 2;
  ctx.fillStyle = '#1B2838'; ctx.beginPath(); ctx.arc(ccx, ccy, r, 0, Math.PI*2); ctx.fill();
  ctx.strokeStyle = '#FFF'; ctx.lineWidth = 3;
  ctx.beginPath(); ctx.moveTo(ccx-r*0.65,ccy-r*0.65); ctx.lineTo(ccx+r*0.65,ccy+r*0.65); ctx.moveTo(ccx+r*0.65,ccy-r*0.65); ctx.lineTo(ccx-r*0.65,ccy+r*0.65); ctx.stroke();
  // Blue left triangle
  ctx.fillStyle = '#2196F3'; ctx.beginPath();
  ctx.moveTo(ccx-r*0.55, ccy-r*0.45); ctx.lineTo(ccx-2, ccy); ctx.lineTo(ccx-r*0.55, ccy+r*0.45); ctx.closePath(); ctx.fill();
  // Dark right triangle
  ctx.fillStyle = '#1B2838'; ctx.beginPath();
  ctx.moveTo(ccx+r*0.55, ccy-r*0.45); ctx.lineTo(ccx+2, ccy); ctx.lineTo(ccx+r*0.55, ccy+r*0.45); ctx.closePath(); ctx.fill();
  ctx.strokeStyle = '#FFF'; ctx.lineWidth = 1.5; ctx.beginPath(); ctx.arc(ccx, ccy, r, 0, Math.PI*2); ctx.stroke();
  if (st === FS.ATK_SPECIAL || st === FS.ATK_SUPER) {
    ctx.fillStyle = 'rgba(108,59,255,0.5)';
    for (let i = 0; i < 5; i++) {
      const px = ccx - 10 - i*8 + Math.sin(fc*0.3+i)*3, py = ccy + Math.cos(fc*0.2+i*2)*6;
      ctx.beginPath(); ctx.arc(px, py, 2, 0, Math.PI*2); ctx.fill();
    }
  }
}

function drawVUALTOBody(ctx, cx, by, bw, bh, fc, st) {
  ctx.fillStyle = '#00B4D8'; roundRect(ctx, cx-bw/2, by, bw, bh, 3); ctx.fill();
  ctx.strokeStyle = '#0077A8'; ctx.lineWidth = 2; roundRect(ctx, cx-bw/2, by, bw, bh, 3); ctx.stroke();
  // V and U geometric paths
  const x = cx - bw/2;
  ctx.fillStyle = '#FFF';
  // V
  ctx.beginPath();
  ctx.moveTo(x+4, by+5); ctx.lineTo(x+12, by+30); ctx.lineTo(x+20, by+5);
  ctx.lineTo(x+16, by+5); ctx.lineTo(x+12, by+22); ctx.lineTo(x+8, by+5);
  ctx.closePath(); ctx.fill();
  // U
  ctx.beginPath();
  ctx.moveTo(x+22, by+5); ctx.lineTo(x+22, by+22);
  ctx.quadraticCurveTo(x+22, by+30, x+29, by+30);
  ctx.quadraticCurveTo(x+36, by+30, x+36, by+22);
  ctx.lineTo(x+36, by+5); ctx.lineTo(x+32, by+5); ctx.lineTo(x+32, by+21);
  ctx.quadraticCurveTo(x+32, by+26, x+29, by+26);
  ctx.quadraticCurveTo(x+26, by+26, x+26, by+21);
  ctx.lineTo(x+26, by+5); ctx.closePath(); ctx.fill();
  if (st === FS.ATK_SPECIAL || st === FS.THROW) {
    const rr = 20 + (fc % 30);
    ctx.strokeStyle = `rgba(0,180,216,${1-(fc%30)/30})`; ctx.lineWidth = 2;
    ctx.beginPath(); ctx.arc(cx, by+bh/2, rr, 0, Math.PI*2); ctx.stroke();
  }
}

function drawInPlayerBody(ctx, cx, by, bw, bh, fc, st) {
  const ccx = cx, ccy = by + bh/2, r = Math.min(bw, bh)/2 - 2;
  const grad = ctx.createLinearGradient(ccx-r, ccy-r, ccx+r, ccy+r);
  grad.addColorStop(0, '#FF0066'); grad.addColorStop(0.5, '#FF4444'); grad.addColorStop(1, '#CC2255');
  ctx.fillStyle = grad; ctx.beginPath(); ctx.arc(ccx, ccy, r, 0, Math.PI*2); ctx.fill();
  // Diagonal shadow
  ctx.fillStyle = 'rgba(100,0,30,0.25)'; ctx.beginPath();
  ctx.moveTo(ccx-r*0.3, ccy+r); ctx.lineTo(ccx+r, ccy-r*0.3); ctx.lineTo(ccx+r, ccy+r); ctx.closePath(); ctx.fill();
  // Play triangle
  const ts = r * 0.55;
  ctx.fillStyle = '#FFF'; ctx.beginPath();
  ctx.moveTo(ccx-ts*0.4, ccy-ts*0.7); ctx.lineTo(ccx+ts*0.8, ccy); ctx.lineTo(ccx-ts*0.4, ccy+ts*0.7);
  ctx.closePath(); ctx.fill();
  if (st === FS.BLOCKING || st === FS.CROUCH_BLOCKING) {
    const fl = Math.sin(fc * 0.6) * 0.4 + 0.4;
    ctx.strokeStyle = `rgba(255,255,255,${fl})`; ctx.lineWidth = 3;
    ctx.beginPath(); ctx.arc(ccx, ccy, r+4, 0, Math.PI*2); ctx.stroke();
  }
}

function drawAugXLabsBody(ctx, cx, by, bw, bh, fc, st) {
  ctx.fillStyle = '#000000'; roundRect(ctx, cx-bw/2, by, bw, bh, 4); ctx.fill();
  ctx.strokeStyle = '#FFD700'; ctx.lineWidth = 1; roundRect(ctx, cx-bw/2, by, bw, bh, 4); ctx.stroke();
  // A mark
  const ay = by + bh/2;
  ctx.lineCap = 'round'; ctx.lineWidth = 5;
  ctx.strokeStyle = '#7B3FBF'; ctx.beginPath(); ctx.moveTo(cx-10, ay+12); ctx.lineTo(cx-2, ay-14); ctx.stroke();
  ctx.strokeStyle = '#9B59F0'; ctx.beginPath(); ctx.moveTo(cx+2, ay-14); ctx.lineTo(cx+10, ay+12); ctx.stroke();
  if (st && st.startsWith && (st.startsWith('ATK') || st === FS.ATK_SPECIAL || st === FS.ATK_SUPER)) {
    ctx.fillStyle = '#FFD700';
    for (let i = 0; i < 4; i++) {
      const sx = cx + Math.sin(fc*0.8+i*1.5)*20, sy2 = ay + Math.cos(fc*0.6+i*2)*16;
      ctx.fillRect(sx-1, sy2-1, 2, 2);
    }
  }
  if (st === FS.ATK_SUPER) {
    const fl = (fc % 6 < 3) ? 0.4 : 0;
    ctx.fillStyle = `rgba(255,215,0,${fl})`; roundRect(ctx, cx-bw/2, by, bw, bh, 4); ctx.fill();
  }
}

function drawQuantumPathBody(ctx, cx, by, bw, bh, fc, st) {
  const ccx = cx, ccy = by + bh/2, r = Math.min(bw, bh)/2 - 2;
  ctx.fillStyle = '#0A1628'; ctx.beginPath(); ctx.arc(ccx, ccy, r, 0, Math.PI*2); ctx.fill();
  // Orbital rings
  ctx.strokeStyle = '#1B3A5C'; ctx.lineWidth = 1.5;
  for (let i = 1; i <= 3; i++) {
    const rr = r * (i / 3.5);
    const sa = fc * 0.02 * (i % 2 === 0 ? 1 : -1);
    ctx.beginPath(); ctx.arc(ccx, ccy, rr, sa, sa + Math.PI*1.6); ctx.stroke();
  }
  // Orbiting dots
  ctx.fillStyle = '#1B3A5C';
  for (let i = 1; i <= 3; i++) {
    const rr = r * (i / 3.5);
    const a = fc * 0.03 * (i % 2 === 0 ? -1 : 1) + i * 2;
    ctx.beginPath(); ctx.arc(ccx + Math.cos(a)*rr, ccy + Math.sin(a)*rr, 2, 0, Math.PI*2); ctx.fill();
  }
  // Center dot
  ctx.fillStyle = '#2196F3'; ctx.beginPath(); ctx.arc(ccx, ccy, 3, 0, Math.PI*2); ctx.fill();
  ctx.strokeStyle = '#1B3A5C'; ctx.lineWidth = 2; ctx.beginPath(); ctx.arc(ccx, ccy, r, 0, Math.PI*2); ctx.stroke();
  if (st === FS.ATK_SPECIAL || st === FS.ATK_SUPER) {
    ctx.fillStyle = '#00FF88'; ctx.font = '6px monospace';
    for (let i = 0; i < 6; i++) {
      const dx = ccx - 14 + i*6, dy = ccy - 16 + ((fc*2+i*7) % 36);
      ctx.fillText(((fc+i*3)%2).toString(), dx, dy);
    }
  }
}

function drawContinent(ctx, ox, oy, pts) {
  if (pts.length < 3) return;
  ctx.beginPath(); ctx.moveTo(ox+pts[0][0], oy+pts[0][1]);
  for (let i = 1; i < pts.length; i++) ctx.lineTo(ox+pts[i][0], oy+pts[i][1]);
  ctx.closePath(); ctx.fill();
}

function drawHELLOBody(ctx, cx, by, bw, bh, fc, st, hpRatio) {
  const ccy = by + bh/2, r = 36;
  // Atmosphere glow
  ctx.fillStyle = 'rgba(135,206,235,0.15)'; ctx.beginPath(); ctx.arc(cx, ccy, r+4, 0, Math.PI*2); ctx.fill();
  // Ocean
  ctx.fillStyle = '#1A6EBD'; ctx.beginPath(); ctx.arc(cx, ccy, r, 0, Math.PI*2); ctx.fill();
  // Clip
  ctx.save(); ctx.beginPath(); ctx.arc(cx, ccy, r, 0, Math.PI*2); ctx.clip();
  // Continents
  const rs = (st === FS.ATK_SPECIAL || st === FS.ATK_SUPER) ? 3 : 0.5;
  const ro = (fc * rs) % (r * 4);
  ctx.fillStyle = '#2D8A4E';
  const c1 = [[0,0],[18,0],[22,8],[16,18],[8,22],[0,16],[-4,8]];
  const c2 = [[0,0],[8,-4],[12,4],[10,16],[4,20],[-2,12]];
  const c3 = [[0,0],[6,0],[8,4],[4,8],[0,6]];
  drawContinent(ctx, cx-20+ro%(r*2)-r, ccy-12, c1);
  drawContinent(ctx, cx+10+ro%(r*2)-r, ccy-6, c2);
  drawContinent(ctx, cx-30+ro%(r*2)-r, ccy+10, c3);
  drawContinent(ctx, cx-20+ro%(r*2)-r+r*2, ccy-12, c1);
  drawContinent(ctx, cx+10+ro%(r*2)-r+r*2, ccy-6, c2);
  // HELLO text
  ctx.fillStyle = '#FFF'; ctx.font = 'bold 14px monospace'; ctx.textAlign = 'center'; ctx.textBaseline = 'middle';
  ctx.strokeStyle = '#000'; ctx.lineWidth = 2;
  const to = -(fc * rs * 0.8) % 80;
  ctx.strokeText('HELLO', cx+to, ccy+2); ctx.fillText('HELLO', cx+to, ccy+2);
  ctx.strokeText('HELLO', cx+to+80, ccy+2); ctx.fillText('HELLO', cx+to+80, ccy+2);
  ctx.restore();
  // Edge highlight
  ctx.strokeStyle = 'rgba(255,255,255,0.2)'; ctx.lineWidth = 2;
  ctx.beginPath(); ctx.arc(cx, ccy, r-1, -0.4, 0.4); ctx.stroke();
  // Crack effect
  if (hpRatio !== undefined && hpRatio < 0.75) {
    ctx.strokeStyle = '#FF4444'; ctx.lineWidth = 1;
    const numCracks = Math.floor((1 - hpRatio) * 5);
    for (let c = 0; c < numCracks; c++) {
      ctx.beginPath();
      ctx.moveTo(cx - 5 + c*6, ccy - r); ctx.lineTo(cx + 3 + c*3, ccy - 8);
      ctx.lineTo(cx - 2 + c*4, ccy + 6); ctx.lineTo(cx + 8 - c*2, ccy + r);
      ctx.stroke();
    }
  }
}

const BODY_RENDERERS = [drawJWXBody, drawJWPlayerBody, drawConnatixBody, drawVUALTOBody, drawInPlayerBody, drawAugXLabsBody, drawQuantumPathBody, drawHELLOBody];

function drawCharacter(ctx, fighter, camX) {
  const ch = CHARACTERS[fighter.charIndex];
  const cx = fighter.x - camX;
  const cy = fighter.y;
  const isHello = fighter.charIndex === CHAR.HELLO;
  const bw = isHello ? 48 : 40;
  const bh = isHello ? 48 : 36;
  const off = getAnimOffsets(fighter.state, frameCount);
  const bodyTop = cy - (isHello ? 70 : 56) + off.bodyY;
  const facingRight = fighter.facingRight;
  const limbColor = ch.colors.limbs;
  const jointColor = ch.colors.joints;
  const armW = isHello ? 14 : 10;
  const armH = isHello ? 22 : 16;
  const legW = isHello ? 14 : 10;
  const legH = isHello ? 24 : 18;

  // Invisible effect (Quantum Path super)
  if (fighter.invisible && fighter.invisible > 0) {
    ctx.globalAlpha = 0.15;
  }
  // Hit flash
  if (fighter.hitFlash > 0) {
    ctx.globalAlpha = 0.6;
  }

  ctx.save();
  if (!facingRight) {
    ctx.translate(cx, 0);
    ctx.scale(-1, 1);
    ctx.translate(-cx, 0);
  }

  // Shadow
  ctx.fillStyle = 'rgba(0,0,0,0.3)'; ctx.beginPath();
  ctx.ellipse(cx, PHYSICS.GROUND_Y + 2, isHello ? 32 : 20, 4, 0, 0, Math.PI * 2); ctx.fill();

  // Legs
  ctx.fillStyle = limbColor;
  ctx.fillRect(cx - 12, bodyTop + bh + 4 + off.legLY, legW, legH);
  ctx.fillRect(cx + 2, bodyTop + bh + 4 + off.legRY, legW, legH);

  // Left arm (behind body)
  ctx.fillStyle = limbColor;
  ctx.fillRect(cx - bw/2 - 4 - armW + off.armLX, bodyTop + 4 + off.armLY, armW, armH);
  ctx.fillStyle = jointColor; ctx.beginPath();
  ctx.arc(cx - bw/2 - 4 - armW/2 + off.armLX, bodyTop + 6 + off.armLY, 2, 0, Math.PI*2); ctx.fill();

  // Body
  if (isHello) {
    drawHELLOBody(ctx, cx, bodyTop, bw, bh, frameCount, fighter.state, fighter.hp / 300);
  } else {
    BODY_RENDERERS[fighter.charIndex](ctx, cx, bodyTop, bw, bh, frameCount, fighter.state);
  }

  // Right arm (in front)
  ctx.fillStyle = limbColor;
  ctx.fillRect(cx + bw/2 + 4 + off.armRX, bodyTop + 4 + off.armRY, armW, armH);
  ctx.fillStyle = jointColor; ctx.beginPath();
  ctx.arc(cx + bw/2 + 4 + armW/2 + off.armRX, bodyTop + 6 + off.armRY, 2, 0, Math.PI*2); ctx.fill();

  ctx.restore();

  ctx.globalAlpha = 1;

  // Augmented Fury size effect
  if (fighter.powerUp && fighter.powerUp > 0) {
    ctx.fillStyle = 'rgba(255,215,0,0.15)';
    ctx.beginPath(); ctx.arc(cx, cy - 30, 40, 0, Math.PI * 2); ctx.fill();
  }
}


// ═══════════════════════════════════════════
// SECTION 8: FIGHTER CLASS
// ═══════════════════════════════════════════

class Fighter {
  constructor(charIndex, playerIndex, startX) {
    this.charIndex = charIndex;
    this.playerIndex = playerIndex;
    const ch = CHARACTERS[charIndex];
    this.x = startX;
    this.y = PHYSICS.GROUND_Y;
    this.vx = 0;
    this.vy = 0;
    this.hp = ch.stats.hp;
    this.maxHp = ch.stats.hp;
    this.displayedHp = ch.stats.hp;
    this.ghostHp = ch.stats.hp;
    this.ghostHpDelay = 0;
    this.superMeter = 0;
    this.state = FS.IDLE;
    this.stateFrame = 0;
    this.facingRight = playerIndex === 0;
    this.onGround = true;
    this.hasHit = false;
    this.comboCount = 0;
    this.lastHitFrame = -100;
    this.speed = ch.stats.speed;
    this.attackMult = ch.stats.attack;
    this.roundsWon = 0;
    this.hitFlash = 0;
    this.invisible = 0;
    this.powerUp = 0;
    this.barrier = 0;
    this.specialType = null;
    this.aiNextThinkFrame = 0;
    this.aiCounters = { playerJumps: 0, playerFireballs: 0, jumpTimestamp: 0, lastThrowFrame: -100 };
    this.dashDir = 0;
    this.dashTimer = 0;
    this.parryWindow = 0;
  }

  setState(newState) {
    this.state = newState;
    this.stateFrame = 0;
    this.hasHit = false;
  }

  getFrameData() {
    return FRAME_DATA[this.state] || null;
  }

  isAttacking() {
    return this.state.startsWith('ATK') || this.state === FS.THROW;
  }

  isActionable() {
    return this.state === FS.IDLE || this.state === FS.WALKING || this.state === FS.CROUCHING;
  }

  canCancel() {
    if (this.state === FS.ATK_LP || this.state === FS.ATK_LK || this.state === FS.ATK_CROUCH_LP) {
      const fd = this.getFrameData();
      if (fd && this.stateFrame >= fd.startup + fd.active) return true;
    }
    return false;
  }

  update(dt, fc, opponent) {
    this.stateFrame++;

    // State machine - auto-advance
    const fd = this.getFrameData();
    if (fd) {
      const total = fd.startup + fd.active + fd.recovery;
      if (this.stateFrame >= total) {
        this.setState(this.onGround ? FS.IDLE : FS.JUMPING);
      }
    }

    // HIT_STUN / KNOCKDOWN / RISING auto-advance
    if (this.state === FS.HIT_STUN && this.stateFrame >= 20) this.setState(FS.IDLE);
    if (this.state === FS.KNOCKDOWN && this.stateFrame >= 40) this.setState(FS.RISING);
    if (this.state === FS.RISING && this.stateFrame >= 20) this.setState(FS.IDLE);
    if (this.state === FS.THROWN && this.stateFrame >= 35) this.setState(this.onGround ? FS.IDLE : FS.JUMPING);
    if (this.state === FS.THROW && this.stateFrame >= 25) this.setState(FS.IDLE);
    if (this.state === FS.DASHING) {
      this.dashTimer -= dt;
      if (this.dashTimer <= 0) this.setState(this.onGround ? FS.IDLE : FS.JUMPING);
    }
    // BLOCKING: player releases when key is up, AI releases after a set duration
    if (this.state === FS.BLOCKING || this.state === FS.CROUCH_BLOCKING) {
      if (this.playerIndex === 0) {
        // Player: release block when block key is released
        const holdingBlock = keys['o'] || keys['O'] || keys['l'] || keys['L'];
        if (!holdingBlock) this.setState(FS.IDLE);
      } else {
        // AI: hold block for a limited time then return to idle
        if (this.stateFrame >= 30) this.setState(FS.IDLE);
      }
    }
    // CROUCHING: return to idle when down is released (player only)
    if (this.state === FS.CROUCHING && this.playerIndex === 0) {
      const holdingDown = keys['ArrowDown'] || keys['s'] || keys['S'];
      if (!holdingDown) this.setState(FS.IDLE);
    }

    // Physics
    if (!this.onGround) {
      this.vy += PHYSICS.GRAVITY * dt;
      if (this.vy > PHYSICS.MAX_FALL_SPEED) this.vy = PHYSICS.MAX_FALL_SPEED;
    }

    // Velocity from state
    if (this.state === FS.WALKING) {
      // Default: walk toward opponent (used by AI)
      this.vx = (this.facingRight ? 1 : -1) * PHYSICS.WALK_SPEED * this.speed;
      // Player 1 overrides with actual key input
      if (this.playerIndex === 0) {
        const left = keys['ArrowLeft'] || keys['a'] || keys['A'];
        const right = keys['ArrowRight'] || keys['d'] || keys['D'];
        if (left && !right) this.vx = -PHYSICS.WALK_SPEED * this.speed;
        else if (right && !left) this.vx = PHYSICS.WALK_SPEED * this.speed;
      }
    } else if (this.state === FS.DASHING) {
      this.vx = this.dashDir * PHYSICS.DASH_SPEED;
    } else if (this.state === FS.HIT_STUN || this.state === FS.KNOCKDOWN || this.state === FS.THROWN) {
      this.vx *= 0.92;
    } else if (!this.isAttacking() && this.state !== FS.BLOCKING && this.state !== FS.CROUCH_BLOCKING) {
      this.vx *= 0.85;
    } else {
      this.vx *= 0.9;
    }

    this.x += this.vx * dt;
    this.y += this.vy * dt;

    // Ground check
    if (this.y >= PHYSICS.GROUND_Y) {
      this.y = PHYSICS.GROUND_Y;
      if (!this.onGround) {
        this.onGround = true;
        if (this.state === FS.JUMPING || this.state === FS.ATK_AIR_LP || this.state === FS.ATK_AIR_HK) {
          this.setState(FS.IDLE);
        }
      }
      this.vy = 0;
    } else {
      this.onGround = false;
    }

    // Boundaries — clamp to both stage limits and visible camera area
    const camLeft = camera.x + 20;
    const camRight = camera.x + CANVAS_W - 20;
    this.x = clamp(this.x, Math.max(PHYSICS.LEFT_BOUNDARY, camLeft), Math.min(PHYSICS.RIGHT_BOUNDARY, camRight));

    // Face opponent — always, even in the air (auto-turn on crossup)
    if (opponent && this.state !== FS.THROW && this.state !== FS.THROWN) {
      this.facingRight = this.x < opponent.x;
    }

    // Push apart — only when both are on the ground (allows jumping over)
    if (opponent && this.onGround && opponent.onGround) {
      const dist = Math.abs(this.x - opponent.x);
      if (dist < PHYSICS.PUSH_DISTANCE) {
        const push = (PHYSICS.PUSH_DISTANCE - dist) / 2;
        if (this.x < opponent.x) { this.x -= push; opponent.x += push; }
        else { this.x += push; opponent.x -= push; }
        // Re-clamp both after push
        this.x = clamp(this.x, PHYSICS.LEFT_BOUNDARY, PHYSICS.RIGHT_BOUNDARY);
        opponent.x = clamp(opponent.x, PHYSICS.LEFT_BOUNDARY, PHYSICS.RIGHT_BOUNDARY);
      }
    }

    // Ghost HP — fast drain on KO so the bar visually empties before round ends
    if (this.hp <= 0) {
      this.ghostHp = lerp(this.ghostHp, 0, 0.15);
      if (this.ghostHp < 1) this.ghostHp = 0;
    } else if (this.ghostHpDelay > 0) {
      this.ghostHpDelay -= dt;
    } else if (this.ghostHp > this.hp) {
      this.ghostHp = lerp(this.ghostHp, this.hp, 0.03);
    }
    this.displayedHp = this.hp;

    // Hit flash
    if (this.hitFlash > 0) this.hitFlash--;

    // Timers
    if (this.invisible > 0) this.invisible--;
    if (this.powerUp > 0) this.powerUp--;
    if (this.barrier > 0) this.barrier--;
    if (this.parryWindow > 0) this.parryWindow--;

    // Combo reset
    if (fc - this.lastHitFrame > 10 && this.comboCount > 0) {
      this.comboCount = 0;
    }
  }

  getHitbox() {
    const fd = this.getFrameData();
    if (!fd || this.hasHit) return null;
    if (this.stateFrame < fd.startup) return null;
    if (this.stateFrame >= fd.startup + fd.active) return null;
    const dir = this.facingRight ? 1 : -1;
    return {
      x: this.x + fd.hitboxX * dir - (dir < 0 ? fd.hitboxW : 0),
      y: this.y - 40 + (fd.hitboxY || 0),
      w: fd.hitboxW, h: fd.hitboxH,
      damage: fd.damage * this.attackMult * (this.powerUp > 0 ? 1.5 : 1),
      stun: fd.stun,
      knockbackX: fd.knockbackX * dir,
      knockbackY: fd.knockbackY || 0,
      type: fd.type,
      knockdown: fd.knockdown || false,
    };
  }

  getHurtbox() {
    const w = this.charIndex === CHAR.HELLO ? 44 : 32;
    const h = (this.state === FS.CROUCHING || this.state === FS.CROUCH_BLOCKING || this.state === FS.ATK_CROUCH_LP || this.state === FS.ATK_CROUCH_HK) ? 30 : 50;
    return { x: this.x - w / 2, y: this.y - h, w, h };
  }

  takeHit(hitbox, attackerX, comboScaling) {
    const scaling = comboScaling || 1;
    const dmg = Math.round(hitbox.damage * scaling);
    this.hp = Math.max(0, this.hp - dmg);
    this.ghostHpDelay = 0.5;
    this.vx = hitbox.knockbackX;
    this.vy = hitbox.knockbackY || 0;
    if (hitbox.knockdown || this.hp <= 0) {
      this.setState(FS.KNOCKDOWN);
      this.vy = -200;
    } else {
      this.setState(FS.HIT_STUN);
    }
    this.hitFlash = 4;
    this.superMeter = Math.min(100, this.superMeter + 8);
    return dmg;
  }

  takeChipDamage(amount) {
    this.hp = Math.max(0, this.hp - Math.round(amount));
  }
}


// ═══════════════════════════════════════════
// SECTION 9: STAGE BACKGROUND RENDERERS
// ═══════════════════════════════════════════

// Ambient particles for stages (separate from combat particles)
const ambientParticles = [];

function resetAmbientParticles(stageIndex) {
  ambientParticles.length = 0;
  const count = 20;
  for (let i = 0; i < count; i++) {
    ambientParticles.push({
      x: Math.random() * STAGE_WIDTH, y: Math.random() * CANVAS_H,
      vx: (Math.random() - 0.3) * 20, vy: -10 - Math.random() * 20,
      size: 1 + Math.random(), life: 999, stage: stageIndex,
    });
  }
}

function updateAmbientParticles(dt, stageIndex) {
  for (const p of ambientParticles) {
    p.x += p.vx * dt; p.y += p.vy * dt;
    // Stage-specific behavior
    if (stageIndex === 1) { p.vy = 60 + Math.random() * 20; p.vx = -5; } // Rain
    else if (stageIndex === 5) { p.vy = 40; p.vx = 0; } // Matrix digits fall
    else { p.vy = -10 - Math.random() * 5; } // Float up
    if (p.y < -10) { p.y = CANVAS_H + 10; p.x = Math.random() * STAGE_WIDTH; }
    if (p.y > CANVAS_H + 10) { p.y = -10; p.x = Math.random() * STAGE_WIDTH; }
  }
}

function drawStageBackground(ctx, stageIndex, camX) {
  const stage = STAGES[stageIndex];
  const isGlobe = stageIndex === 7;

  // Far layer (0.2x)
  ctx.save();
  if (!isGlobe) ctx.translate(-camX * 0.2, 0);
  drawStageFar(ctx, stageIndex);
  ctx.restore();

  // Mid layer (0.5x)
  ctx.save();
  if (!isGlobe) ctx.translate(-camX * 0.5, 0);
  drawStageMid(ctx, stageIndex);
  ctx.restore();

  // Near layer (0.8x)
  ctx.save();
  if (!isGlobe) ctx.translate(-camX * 0.8, 0);
  drawStageNear(ctx, stageIndex);
  ctx.restore();

  // Floor
  drawStageFloor(ctx, stageIndex, camX);

  // Ambient particles
  for (const p of ambientParticles) {
    const sx = p.x - camX * 0.5;
    if (sx < -5 || sx > CANVAS_W + 5) continue;
    ctx.globalAlpha = 0.6;
    if (stageIndex === 1) { // Rain
      ctx.strokeStyle = 'rgba(108,59,255,0.3)'; ctx.lineWidth = 1;
      ctx.beginPath(); ctx.moveTo(sx, p.y); ctx.lineTo(sx - 1, p.y + 8); ctx.stroke();
    } else if (stageIndex === 5) { // Matrix
      ctx.fillStyle = '#00FF44'; ctx.font = '6px monospace';
      ctx.fillText(Math.random() > 0.5 ? '1' : '0', sx, p.y);
    } else {
      ctx.fillStyle = stage.accentColor || '#FFF';
      ctx.fillRect(sx, p.y, p.size, p.size);
    }
    ctx.globalAlpha = 1;
  }
}

function drawStageFar(ctx, si) {
  const s = STAGES[si];
  ctx.fillStyle = s.bgColor;
  ctx.fillRect(0, 0, STAGE_WIDTH, PHYSICS.GROUND_Y);

  if (si === 0) { // Broadcast - dark studio, screens
    ctx.fillStyle = '#0A1220';
    ctx.fillRect(0, 0, STAGE_WIDTH, PHYSICS.GROUND_Y);
    for (let i = 0; i < 6; i++) {
      ctx.fillStyle = '#111828'; ctx.fillRect(80 + i * 140, 30, 80, 50);
      ctx.fillStyle = (frameCount % 120 < 60) ? '#FF4500' : '#CC3700';
      ctx.fillRect(84 + i * 140, 34, 72, 42);
      // Play button on screen
      ctx.fillStyle = '#FFF';
      ctx.beginPath(); ctx.moveTo(110+i*140, 48); ctx.lineTo(130+i*140, 55); ctx.lineTo(110+i*140, 62); ctx.closePath(); ctx.fill();
    }
  } else if (si === 1) { // Ad alley - neon city
    ctx.fillStyle = '#0D0020'; ctx.fillRect(0, 0, STAGE_WIDTH, PHYSICS.GROUND_Y);
    // Buildings
    for (let i = 0; i < 10; i++) {
      const bh = 60 + Math.sin(i * 2.3) * 30;
      ctx.fillStyle = `hsl(${260 + i * 5}, 30%, ${8 + i}%)`;
      ctx.fillRect(i * 100, PHYSICS.GROUND_Y - bh, 80, bh);
    }
  } else if (si === 2) { // Stream vault - server racks
    ctx.fillStyle = '#1A2430'; ctx.fillRect(0, 0, STAGE_WIDTH, PHYSICS.GROUND_Y);
    for (let i = 0; i < 12; i++) {
      ctx.fillStyle = '#222E3A'; ctx.fillRect(20 + i * 80, 20, 60, 180);
      // LED grid
      for (let r = 0; r < 12; r++) for (let c = 0; c < 4; c++) {
        ctx.fillStyle = ((frameCount + i * 3 + r * 7 + c * 13) % 60 < 30) ? '#00FF44' : '#00B4D8';
        ctx.fillRect(30 + i * 80 + c * 12, 30 + r * 14, 3, 3);
      }
    }
  } else if (si === 3) { // Paywall plaza
    ctx.fillStyle = '#3A0818'; ctx.fillRect(0, 0, STAGE_WIDTH, PHYSICS.GROUND_Y);
    // Gate
    ctx.fillStyle = '#2A0610'; ctx.fillRect(400, 30, 160, 160);
    ctx.strokeStyle = '#FFD700'; ctx.lineWidth = 3;
    ctx.strokeRect(410, 35, 140, 150);
    ctx.fillStyle = '#FFD700'; ctx.font = 'bold 10px monospace'; ctx.textAlign = 'center';
    ctx.fillText('PREMIUM ACCESS', 480, 50);
    // Padlock
    ctx.fillStyle = '#888'; ctx.fillRect(465, 100, 30, 25);
    ctx.strokeStyle = '#888'; ctx.lineWidth = 3; ctx.beginPath();
    ctx.arc(480, 100, 12, Math.PI, 0); ctx.stroke();
  } else if (si === 4) { // AI Lab
    ctx.fillStyle = '#E8E8E8'; ctx.fillRect(0, 0, STAGE_WIDTH, PHYSICS.GROUND_Y);
    // Circuit traces
    ctx.strokeStyle = '#FF6B00'; ctx.lineWidth = 1;
    for (let i = 0; i < 20; i++) {
      ctx.beginPath();
      ctx.moveTo(i * 50, 20 + Math.sin(i) * 40);
      ctx.lineTo(i * 50 + 30, 60 + Math.cos(i * 1.5) * 30);
      ctx.lineTo(i * 50 + 50, 40 + Math.sin(i * 2) * 20);
      ctx.stroke();
    }
  } else if (si === 5) { // Data grid - Matrix
    ctx.fillStyle = '#000'; ctx.fillRect(0, 0, STAGE_WIDTH, PHYSICS.GROUND_Y);
    // Perspective grid
    ctx.strokeStyle = '#003300'; ctx.lineWidth = 1;
    for (let i = 0; i < 20; i++) {
      ctx.beginPath(); ctx.moveTo(i * 50, 0); ctx.lineTo(i * 50 - 100, PHYSICS.GROUND_Y); ctx.stroke();
    }
    for (let i = 0; i < 10; i++) {
      const y = 20 + i * 20;
      ctx.beginPath(); ctx.moveTo(0, y); ctx.lineTo(STAGE_WIDTH, y); ctx.stroke();
    }
  } else if (si === 6) { // Mirror
    ctx.fillStyle = '#B0B0B0'; ctx.fillRect(0, 0, STAGE_WIDTH, PHYSICS.GROUND_Y);
    // Chrome cubes
    for (let i = 0; i < 8; i++) {
      const cx2 = 60 + i * 120 + Math.sin(frameCount * 0.01 + i) * 20;
      const cy2 = 60 + Math.cos(frameCount * 0.015 + i * 2) * 30;
      ctx.fillStyle = '#D0D0D0'; ctx.fillRect(cx2, cy2, 20, 20);
      ctx.fillStyle = '#E8E8E8'; ctx.fillRect(cx2, cy2, 20, 10);
    }
  } else if (si === 7) { // Globe arena - space
    ctx.fillStyle = '#000010'; ctx.fillRect(0, 0, CANVAS_W, CANVAS_H);
    // Stars
    for (let i = 0; i < 40; i++) {
      const sx = (i * 37 + 13) % CANVAS_W;
      const sy = (i * 23 + 7) % (CANVAS_H - 60);
      const blink = ((frameCount + i * 17) % 120 < 100) ? 1 : 0.3;
      ctx.globalAlpha = blink;
      ctx.fillStyle = '#FFF'; ctx.fillRect(sx, sy, 1, 1);
    }
    ctx.globalAlpha = 1;
    // Earth horizon
    ctx.fillStyle = '#1A6EBD';
    ctx.beginPath(); ctx.arc(CANVAS_W / 2, -200, 300, 0, Math.PI); ctx.fill();
    ctx.fillStyle = '#2D8A4E';
    ctx.beginPath(); ctx.arc(CANVAS_W / 2 - 50, -205, 80, 0.3, 1.2); ctx.fill();
    // Aurora
    ctx.globalAlpha = 0.15;
    const auroraY = 20 + Math.sin(frameCount * 0.02) * 8;
    const aGrad = ctx.createLinearGradient(0, auroraY, 0, auroraY + 40);
    aGrad.addColorStop(0, '#00FFCC'); aGrad.addColorStop(1, 'transparent');
    ctx.fillStyle = aGrad; ctx.fillRect(0, auroraY, CANVAS_W, 40);
    ctx.globalAlpha = 1;
  }
}

function drawStageMid(ctx, si) {
  if (si === 0) { // Broadcast - spotlights
    ctx.globalAlpha = 0.1;
    for (let i = 0; i < 4; i++) {
      const sx = 120 + i * 200 + Math.sin(frameCount * 0.02 + i) * 40;
      ctx.fillStyle = '#FFFFEE';
      ctx.beginPath(); ctx.moveTo(sx, 20); ctx.lineTo(sx - 30, PHYSICS.GROUND_Y); ctx.lineTo(sx + 30, PHYSICS.GROUND_Y); ctx.closePath(); ctx.fill();
    }
    ctx.globalAlpha = 1;
  } else if (si === 1) { // Ad alley - billboards
    const texts = ['BUY AD SPACE', 'CPM: 9999', 'CLICK HERE', 'SUBSCRIBE', 'AD TECH'];
    for (let i = 0; i < 5; i++) {
      ctx.fillStyle = '#200040'; ctx.fillRect(60 + i * 180, 50, 120, 30);
      ctx.fillStyle = '#6C3BFF'; ctx.font = '8px monospace'; ctx.textAlign = 'center';
      const ti = (Math.floor(frameCount / 240) + i) % texts.length;
      ctx.fillText(texts[ti], 120 + i * 180, 70);
    }
  } else if (si === 2) { // Stream vault - data streams
    ctx.strokeStyle = 'rgba(0,180,216,0.4)'; ctx.lineWidth = 1;
    for (let i = 0; i < 8; i++) {
      const y = 40 + i * 20;
      const off = (frameCount * 2 + i * 50) % STAGE_WIDTH;
      ctx.beginPath(); ctx.moveTo(off, y); ctx.lineTo(off + 60, y); ctx.stroke();
    }
  } else if (si === 3) { // Paywall - pillars
    for (let i = 0; i < 6; i++) {
      ctx.fillStyle = '#5A1020'; ctx.fillRect(50 + i * 170, 40, 30, 160);
      ctx.fillStyle = '#6A2030'; ctx.fillRect(50 + i * 170, 40, 30, 10);
    }
  } else if (si === 4) { // AI Lab - holograms
    ctx.globalAlpha = 0.3;
    for (let i = 0; i < 4; i++) {
      const hx = 100 + i * 220 + Math.sin(frameCount * 0.015 + i) * 10;
      const hy = 80 + Math.cos(frameCount * 0.02 + i * 2) * 10;
      ctx.strokeStyle = '#FFD700'; ctx.lineWidth = 1;
      ctx.beginPath();
      for (let j = 0; j < 6; j++) {
        const a = j / 6 * Math.PI * 2 + frameCount * 0.01;
        const r = 15;
        const method = j === 0 ? 'moveTo' : 'lineTo';
        ctx[method](hx + Math.cos(a) * r, hy + Math.sin(a) * r);
      }
      ctx.closePath(); ctx.stroke();
    }
    ctx.globalAlpha = 1;
  } else if (si === 5) { // Data grid - floating cubes
    for (let i = 0; i < 6; i++) {
      const cx2 = 80 + i * 150 + Math.sin(frameCount * 0.01 + i * 3) * 30;
      const cy2 = 50 + Math.cos(frameCount * 0.008 + i * 2) * 40;
      ctx.strokeStyle = '#00FF44'; ctx.lineWidth = 1;
      ctx.strokeRect(cx2, cy2, 12, 12);
    }
  } else if (si === 7) { // Globe - satellites
    ctx.globalAlpha = 0.4;
    for (let i = 0; i < 3; i++) {
      const sx = (frameCount * 0.3 + i * 160) % CANVAS_W;
      ctx.fillStyle = '#888'; ctx.fillRect(sx, 30 + i * 15, 6, 3);
      ctx.fillRect(sx + 1, 28 + i * 15, 4, 7);
    }
    ctx.globalAlpha = 1;
  }
}

function drawStageNear(ctx, si) {
  if (si === 0) { // Broadcast - LIVE sign + cables
    // LIVE sign
    ctx.fillStyle = '#200000'; ctx.fillRect(20, 60, 50, 20);
    ctx.fillStyle = (frameCount % 60 < 30) ? '#FF0000' : '#880000';
    ctx.font = 'bold 10px monospace'; ctx.textAlign = 'center';
    ctx.fillText('LIVE', 45, 75);
    // Cables
    ctx.strokeStyle = '#333'; ctx.lineWidth = 2;
    for (let i = 0; i < 5; i++) {
      ctx.beginPath(); ctx.moveTo(i * 200, PHYSICS.GROUND_Y);
      ctx.quadraticCurveTo(i * 200 + 50, PHYSICS.GROUND_Y - 5, i * 200 + 100, PHYSICS.GROUND_Y);
      ctx.stroke();
    }
  } else if (si === 1) { // Ad alley - server boxes
    for (let i = 0; i < 8; i++) {
      ctx.fillStyle = '#1A1A2A'; ctx.fillRect(30 + i * 120, PHYSICS.GROUND_Y - 25, 20, 25);
      // LED
      ctx.fillStyle = ((frameCount + i * 11) % 40 < 20) ? '#0F0' : '#F00';
      ctx.fillRect(35 + i * 120, PHYSICS.GROUND_Y - 22, 3, 3);
    }
  } else if (si === 2) { // Stream vault - warning stripes
    ctx.fillStyle = '#FFD700';
    for (let i = 0; i < STAGE_WIDTH; i += 20) {
      if ((i / 20) % 2 === 0) ctx.fillRect(i, PHYSICS.GROUND_Y - 3, 10, 3);
    }
  } else if (si === 3) { // Paywall - velvet ropes
    ctx.strokeStyle = '#CC0000'; ctx.lineWidth = 2;
    ctx.beginPath(); ctx.moveTo(100, 160); ctx.lineTo(860, 160); ctx.stroke();
  } else if (si === 4) { // AI Lab - workstations
    for (let i = 0; i < 6; i++) {
      ctx.fillStyle = '#DDD'; ctx.fillRect(50 + i * 160, PHYSICS.GROUND_Y - 40, 40, 40);
      ctx.fillStyle = '#333'; ctx.fillRect(54 + i * 160, PHYSICS.GROUND_Y - 36, 32, 24);
      // Code scrolling
      ctx.fillStyle = '#0F0'; ctx.font = '4px monospace';
      for (let r = 0; r < 4; r++) {
        ctx.fillText('var x=0;', 56 + i * 160, PHYSICS.GROUND_Y - 32 + r * 6 + (frameCount % 6));
      }
    }
  }
}

function drawStageFloor(ctx, si, camX) {
  const s = STAGES[si];
  const isGlobe = si === 7;
  if (isGlobe) {
    // Curved surface
    ctx.fillStyle = '#303030';
    ctx.beginPath();
    ctx.moveTo(0, PHYSICS.GROUND_Y);
    ctx.quadraticCurveTo(CANVAS_W / 2, PHYSICS.GROUND_Y + 15, CANVAS_W, PHYSICS.GROUND_Y);
    ctx.lineTo(CANVAS_W, CANVAS_H);
    ctx.lineTo(0, CANVAS_H);
    ctx.closePath(); ctx.fill();
  } else if (si === 3) { // Checkered marble
    for (let x2 = 0; x2 < STAGE_WIDTH; x2 += 16) {
      const sx = x2 - camX;
      if (sx < -16 || sx > CANVAS_W + 16) continue;
      for (let y2 = PHYSICS.GROUND_Y; y2 < CANVAS_H; y2 += 16) {
        ctx.fillStyle = ((x2 / 16 + y2 / 16) % 2 === 0) ? '#4A1828' : '#FFD700';
        ctx.globalAlpha = 0.3;
        ctx.fillRect(sx, y2, 16, 16);
      }
    }
    ctx.globalAlpha = 1;
  } else if (si === 5) { // Grid floor
    ctx.fillStyle = '#000'; ctx.fillRect(0, PHYSICS.GROUND_Y, CANVAS_W, 60);
    ctx.strokeStyle = '#003300'; ctx.lineWidth = 1;
    for (let x2 = 0; x2 < STAGE_WIDTH; x2 += 30) {
      const sx = x2 - camX;
      ctx.beginPath(); ctx.moveTo(sx, PHYSICS.GROUND_Y); ctx.lineTo(sx, CANVAS_H); ctx.stroke();
    }
    for (let y2 = PHYSICS.GROUND_Y; y2 < CANVAS_H; y2 += 15) {
      ctx.beginPath(); ctx.moveTo(0, y2); ctx.lineTo(CANVAS_W, y2); ctx.stroke();
    }
    // Green glow
    ctx.globalAlpha = 0.1;
    ctx.fillStyle = '#00FF44'; ctx.fillRect(0, PHYSICS.GROUND_Y, CANVAS_W, 8);
    ctx.globalAlpha = 1;
  } else if (si === 6) { // Mirror floor
    ctx.fillStyle = '#B0B0B0'; ctx.fillRect(0, PHYSICS.GROUND_Y, CANVAS_W, 60);
    ctx.globalAlpha = 0.1;
    ctx.fillStyle = '#FFF'; ctx.fillRect(0, PHYSICS.GROUND_Y, CANVAS_W, 4);
    ctx.globalAlpha = 1;
  } else {
    ctx.fillStyle = s.floorColor;
    ctx.fillRect(0, PHYSICS.GROUND_Y, CANVAS_W, CANVAS_H - PHYSICS.GROUND_Y);
  }
}


// ═══════════════════════════════════════════
// SECTION 10: HUD RENDERER
// ═══════════════════════════════════════════

const floatingDamage = [];
let announcementText = '';
let announcementTimer = 0;
let announcementScale = 0.5;
let announcementColor = '#FFF';

function showAnnouncement(text, color, duration) {
  announcementText = text;
  announcementColor = color || '#FFF';
  announcementTimer = duration || 90;
  announcementScale = 0.5;
}

function drawHUD(ctx, p1, p2, timer, round) {
  // Health bars
  drawHealthBar(ctx, p1, 10, 8, true);
  drawHealthBar(ctx, p2, CANVAS_W - 10, 8, false);

  // Timer
  const timerSec = Math.ceil(timer);
  ctx.fillStyle = timerSec <= 10 ? '#FF2222' : '#FFFFFF';
  ctx.font = 'bold 20px monospace'; ctx.textAlign = 'center';
  if (timerSec <= 10 && frameCount % 30 < 15) ctx.fillStyle = '#FF6666';
  ctx.fillText(timerSec.toString().padStart(2, '0'), CANVAS_W / 2, 22);

  // Super meters
  drawSuperMeter(ctx, p1, 10, 24, true);
  drawSuperMeter(ctx, p2, CANVAS_W - 10, 24, false);

  // Character names
  ctx.font = '7px monospace';
  ctx.fillStyle = '#FFF'; ctx.textAlign = 'left';
  ctx.fillText(CHARACTERS[p1.charIndex].name, 12, 7);
  ctx.textAlign = 'right';
  ctx.fillText(CHARACTERS[p2.charIndex].name, CANVAS_W - 12, 7);

  // Round indicators
  for (let i = 0; i < 3; i++) {
    ctx.beginPath(); ctx.arc(50 + i * 14, CANVAS_H - 10, 4, 0, Math.PI * 2);
    ctx.fillStyle = i < p1.roundsWon ? '#FFD700' : 'transparent';
    ctx.fill();
    ctx.strokeStyle = '#FFF'; ctx.lineWidth = 1; ctx.stroke();
  }
  for (let i = 0; i < 3; i++) {
    ctx.beginPath(); ctx.arc(CANVAS_W - 50 - i * 14, CANVAS_H - 10, 4, 0, Math.PI * 2);
    ctx.fillStyle = i < p2.roundsWon ? '#FFD700' : 'transparent';
    ctx.fill();
    ctx.strokeStyle = '#FFF'; ctx.lineWidth = 1; ctx.stroke();
  }

  // Round label
  ctx.font = '6px monospace'; ctx.fillStyle = '#AAA'; ctx.textAlign = 'left';
  ctx.fillText(`ROUND ${round}`, 10, CANVAS_H - 16);

  // Combo counter
  if (p1.comboCount >= 2) drawComboCounter(ctx, p2.x - camera.x, '#FFD700', p1.comboCount);
  if (p2.comboCount >= 2) drawComboCounter(ctx, p1.x - camera.x, '#FFD700', p2.comboCount);

  // Floating damage
  for (let i = floatingDamage.length - 1; i >= 0; i--) {
    const fd = floatingDamage[i];
    fd.y -= 0.5; fd.life--;
    if (fd.life <= 0) { floatingDamage.splice(i, 1); continue; }
    ctx.globalAlpha = fd.life / 30;
    ctx.fillStyle = fd.color;
    ctx.font = '8px monospace'; ctx.textAlign = 'center';
    ctx.fillText(`-${fd.amount}`, fd.x - camera.x, fd.y);
    ctx.globalAlpha = 1;
  }

  // Announcement
  if (announcementTimer > 0) {
    announcementTimer--;
    announcementScale = Math.min(1, announcementScale + 0.08);
    ctx.save();
    ctx.translate(CANVAS_W / 2, CANVAS_H / 2 - 20);
    ctx.scale(announcementScale, announcementScale);
    ctx.font = 'bold 28px monospace'; ctx.textAlign = 'center'; ctx.textBaseline = 'middle';
    ctx.fillStyle = '#000';
    ctx.fillText(announcementText, 2, 2);
    ctx.fillStyle = announcementColor;
    ctx.fillText(announcementText, 0, 0);
    ctx.restore();
  }
}

function drawHealthBar(ctx, fighter, x, y, isLeft) {
  const maxW = fighter.charIndex === CHAR.HELLO ? 200 : 160;
  const barH = 10;
  const hp = fighter.hp;
  const maxHp = fighter.maxHp;
  const ghostHp = fighter.ghostHp;

  const barX = isLeft ? x : x - maxW;

  // Background
  ctx.fillStyle = '#333'; roundRect(ctx, barX, y, maxW, barH, 3); ctx.fill();

  // Ghost bar — don't draw if essentially empty
  const ghostW = (ghostHp / maxHp) * maxW;
  if (ghostW > 1) {
    const gx = isLeft ? barX : barX + maxW - ghostW;
    ctx.fillStyle = '#FFFF00';
    if (ghostW > 6) { roundRect(ctx, gx, y, ghostW, barH, 3); ctx.fill(); }
    else { ctx.fillRect(gx, y, ghostW, barH); }
  }

  // Current HP — don't draw if at 0
  const hpRatio = hp / maxHp;
  const hpW = hpRatio * maxW;
  if (hpW > 1) {
    const hx = isLeft ? barX : barX + maxW - hpW;
    let hpColor = '#44CC44';
    if (hpRatio < 0.25) { hpColor = (frameCount % 15 < 8) ? '#FF2222' : '#FF6666'; }
    else if (hpRatio < 0.5) hpColor = '#FFCC00';
    ctx.fillStyle = hpColor;
    if (hpW > 6) { roundRect(ctx, hx, y, hpW, barH, 3); ctx.fill(); }
    else { ctx.fillRect(hx, y, hpW, barH); }
  }

  // Border
  ctx.strokeStyle = '#000'; ctx.lineWidth = 1; roundRect(ctx, barX, y, maxW, barH, 3); ctx.stroke();

  // x3 label for HELLO
  if (fighter.charIndex === CHAR.HELLO) {
    ctx.fillStyle = '#FF0'; ctx.font = 'bold 7px monospace'; ctx.textAlign = isLeft ? 'right' : 'left';
    ctx.fillText('x3', isLeft ? barX + maxW + 12 : barX - 12, y + 8);
  }
}

function drawSuperMeter(ctx, fighter, x, y, isLeft) {
  const maxW = 140;
  const barH = 5;
  const barX = isLeft ? x : x - maxW;
  ctx.fillStyle = '#222'; ctx.fillRect(barX, y, maxW, barH);
  const sw = (fighter.superMeter / 100) * maxW;
  const sx = isLeft ? barX : barX + maxW - sw;
  ctx.fillStyle = '#FFD700'; ctx.fillRect(sx, y, sw, barH);
  if (fighter.superMeter >= 100) {
    ctx.strokeStyle = `rgba(255,255,255,${0.3 + Math.sin(frameCount * 0.2) * 0.3})`;
    ctx.lineWidth = 1; ctx.strokeRect(barX, y, maxW, barH);
  }
  // Label
  ctx.fillStyle = '#888'; ctx.font = '5px monospace';
  ctx.textAlign = isLeft ? 'left' : 'right';
  ctx.fillText('SUPER', isLeft ? barX : barX + maxW, y - 1);
}

function drawComboCounter(ctx, targetX, color, count) {
  const txt = count >= 6 ? `${count}x COMBO` : `${count}x HIT`;
  const scale = 1 + (frameCount % 6 < 3 ? 0.15 : 0);
  let col = '#FFD700';
  if (count >= 9) col = '#FF2200';
  else if (count >= 5) col = '#FF8800';
  ctx.save();
  ctx.translate(clamp(targetX, 60, CANVAS_W - 60), 190);
  ctx.scale(scale, scale);
  ctx.font = 'bold 14px monospace'; ctx.textAlign = 'center';
  ctx.fillStyle = '#000'; ctx.fillText(txt, 1, 1);
  ctx.fillStyle = col; ctx.fillText(txt, 0, 0);
  ctx.restore();
}


// ═══════════════════════════════════════════
// SECTION 11: AI SYSTEM
// ═══════════════════════════════════════════

function updateAI(aiFighter, opponent, fc) {
  if (fc < aiFighter.aiNextThinkFrame) return;

  const fightIdx = currentFightIndex;
  const diff = DIFFICULTY[Math.min(fightIdx, DIFFICULTY.length - 1)];
  const interval = diff.thinkMin + Math.floor(Math.random() * (diff.thinkMax - diff.thinkMin));
  aiFighter.aiNextThinkFrame = fc + interval;

  if (!aiFighter.isActionable()) return;

  const gap = Math.abs(aiFighter.x - opponent.x);
  const profile = CHARACTERS[aiFighter.charIndex].aiProfile;
  const aggression = diff.aggression + (profile.aggressionBias || 0);

  // Wild card randomize
  let dashBias = profile.dashBias || 0;
  let fireballBias = profile.fireballBias || 0;
  let throwBias = profile.throwBias || 0;
  let blockBias = profile.blockBias || 0;
  if (profile.wildCard) {
    dashBias += (Math.random() - 0.5) * 0.3;
    fireballBias += (Math.random() - 0.5) * 0.3;
    throwBias += (Math.random() - 0.5) * 0.3;
  }

  // Priority 1: Danger
  if (aiFighter.hp < 25 && opponent.hp > 50) {
    if (Math.random() < 0.6) { aiBlock(aiFighter); return; }
    if (Math.random() < 0.3) { aiJumpBack(aiFighter); return; }
    if (aiFighter.superMeter >= 100) { aiDoSuper(aiFighter); return; }
  }

  // Priority 2: Super
  if (aiFighter.superMeter >= 100 && gap < 150) {
    if (Math.random() < 0.6) { aiDoSuper(aiFighter); return; }
  }

  // Priority 3: Projectile reaction
  const incoming = projectiles.find(p => p.owner !== aiFighter && Math.abs(p.x - aiFighter.x) < 200 &&
    ((p.vx > 0 && p.x < aiFighter.x) || (p.vx < 0 && p.x > aiFighter.x)));
  if (incoming) {
    const pdist = Math.abs(incoming.x - aiFighter.x);
    if (pdist < 80) { aiJump(aiFighter); return; }
    if (Math.random() < 0.5 + fireballBias) { aiFireball(aiFighter); return; }
    aiJump(aiFighter); return;
  }

  // Priority 4: Anti-air
  if (!opponent.onGround && gap < 150) {
    if (Math.random() < 0.4) { aiDP(aiFighter); return; }
  }

  // Range decisions
  if (gap < 80) {
    // Close
    const r = Math.random();
    if (r < 0.3 + throwBias && fc - aiFighter.aiCounters.lastThrowFrame > 90) {
      aiThrow(aiFighter, fc); return;
    } else if (r < 0.7 + aggression * 0.1) {
      aiAttack(aiFighter, 'light'); return;
    } else if (r < 0.9) {
      aiDP(aiFighter); return;
    } else {
      aiBlock(aiFighter); return;
    }
  } else if (gap < 200) {
    // Mid
    const r = Math.random();
    if (r < 0.35 + dashBias) { aiWalkForward(aiFighter); }
    else if (r < 0.65 + fireballBias) { aiFireball(aiFighter); }
    else if (r < 0.85) { aiDash(aiFighter); }
    else { aiJump(aiFighter); }
  } else {
    // Far
    const r = Math.random();
    if (r < 0.5) { aiWalkForward(aiFighter); }
    else if (r < 0.8 + fireballBias) { aiFireball(aiFighter); }
    else { /* idle */ }
  }

  // Reactive blocking — only if not already blocking (prevents stateFrame reset loop)
  if (opponent.isAttacking() && aiFighter.state !== FS.BLOCKING && aiFighter.state !== FS.CROUCH_BLOCKING) {
    const fd = opponent.getFrameData();
    if (fd && opponent.stateFrame >= fd.startup && opponent.stateFrame < fd.startup + fd.active) {
      if (gap < 150 && Math.random() < diff.blockRate + blockBias) {
        aiBlock(aiFighter);
      }
    }
  }
}

function aiWalkForward(f) {
  f.setState(FS.WALKING);
  f.vx = (f.facingRight ? 1 : -1) * PHYSICS.WALK_SPEED * f.speed;
}
function aiJump(f) { if (f.onGround) { f.setState(FS.JUMPING); f.vy = PHYSICS.JUMP_VELOCITY; f.onGround = false; } }
function aiJumpBack(f) { if (f.onGround) { f.setState(FS.JUMPING); f.vy = PHYSICS.JUMP_VELOCITY; f.vx = (f.facingRight ? -1 : 1) * 100; f.onGround = false; } }
function aiBlock(f) { f.setState(FS.BLOCKING); }
function aiAttack(f, type) { f.setState(type === 'light' ? FS.ATK_LP : FS.ATK_HP); }
function aiThrow(f, fc) { f.setState(FS.THROW); f.aiCounters.lastThrowFrame = fc; }
function aiDash(f) { f.setState(FS.DASHING); f.dashDir = f.facingRight ? 1 : -1; f.dashTimer = PHYSICS.DASH_DURATION; }
function aiAirDash(f) { if (!f.onGround) { f.setState(FS.DASHING); f.dashDir = f.facingRight ? 1 : -1; f.dashTimer = PHYSICS.DASH_DURATION; } }
function aiFireball(f) {
  if (projectiles.some(p => p.owner === f)) return;
  f.setState(FS.ATK_SPECIAL);
  f.specialType = SPECIAL.FIREBALL;
  const dir = f.facingRight ? 1 : -1;
  const ch = CHARACTERS[f.charIndex];
  projectiles.push(new Projectile(f, f.x + dir * 30, f.y - 30, dir * 250, 0, 10, ch.projectileColor, ch.projectileShape));
  SFX.fireballLaunch();
}
function aiDP(f) { f.setState(FS.ATK_SPECIAL); f.vy = PHYSICS.JUMP_VELOCITY * 0.8; f.vx = (f.facingRight ? 1 : -1) * 100; f.onGround = false; }
function aiDoSuper(f) {
  if (f.superMeter < 100) return;
  f.setState(FS.ATK_SUPER);
  f.superMeter = 0;
  SFX.superActivate();
}

// HELLO Boss AI
function updateHelloAI(boss, player, fc) {
  if (fc < boss.aiNextThinkFrame) return;
  if (!boss.isActionable()) return;

  const phase2 = boss.hp <= 150;
  const interval = phase2 ? (6 + Math.floor(Math.random() * 2)) : (8 + Math.floor(Math.random() * 4));
  boss.aiNextThinkFrame = fc + interval;

  const gap = Math.abs(boss.x - player.x);

  // World Spin at 50% HP (one-time)
  if (boss.hp <= 150 && !boss._worldSpinUsed) {
    boss._worldSpinUsed = true;
    boss.setState(FS.ATK_SUPER);
    SFX.superActivate();
    return;
  }

  // Airborne player
  if (!player.onGround) {
    if (Math.random() < 0.5) { // Globe Slam
      boss.setState(FS.ATK_HK); boss.vy = PHYSICS.JUMP_VELOCITY; boss.onGround = false;
    } else {
      aiFireball(boss);
    }
    return;
  }

  if (gap < 70) {
    const r = Math.random();
    if (r < (phase2 ? 0.55 : 0.4)) { aiThrow(boss, fc); } // Orbital Grab
    else if (r < 0.75) { boss.setState(FS.ATK_HP); } // Globe Slam
    else { aiAttack(boss, 'light'); }
  } else if (gap < 200) {
    const r = Math.random();
    const fireRate = phase2 ? 0.55 : 0.4;
    if (r < fireRate) { aiFireball(boss); } // Hello Wave
    else if (r < fireRate + 0.3) { boss.setState(FS.ATK_CROUCH_HK); } // Seismic Stomp
    else if (r < fireRate + 0.5) { aiWalkForward(boss); }
    else { aiDash(boss); }
  } else {
    if (Math.random() < (phase2 ? 0.6 : 0.5)) { aiFireball(boss); }
    else { aiWalkForward(boss); }
  }
}


// ═══════════════════════════════════════════
// SECTION 12: SCREEN RENDERERS
// ═══════════════════════════════════════════

// Title screen stars
const titleStars = [];
for (let i = 0; i < 40; i++) titleStars.push({ x: Math.random() * CANVAS_W, y: Math.random() * CANVAS_H, speed: 0.2 + Math.random() * 0.5 });

function updateTitleScreen(dt) {
  for (const s of titleStars) {
    s.x += s.speed;
    if (s.x > CANVAS_W) s.x = 0;
  }
  if (justPressed['Enter'] || justPressed[' ']) {
    SFX.cursorConfirm();
    setGameState(GS.CHARACTER_SELECT);
  }
}

function renderTitleScreen(ctx) {
  ctx.fillStyle = '#000'; ctx.fillRect(0, 0, CANVAS_W, CANVAS_H);
  // Stars
  ctx.fillStyle = '#FFF';
  for (const s of titleStars) ctx.fillRect(s.x, s.y, 1, 1);
  // Hidden Earth silhouette
  ctx.globalAlpha = 0.04;
  ctx.fillStyle = '#1A6EBD';
  ctx.beginPath(); ctx.arc(CANVAS_W/2, CANVAS_H/2 + 20, 80, 0, Math.PI*2); ctx.fill();
  ctx.globalAlpha = 1;
  // Title
  const titleChars = 'HELLO WORLD';
  const revealed = Math.min(titleChars.length, Math.floor(stateTimer / 6));
  const titleX = CANVAS_W / 2;
  ctx.textAlign = 'center';
  // Glow
  const glowAlpha = 0.3 + Math.sin(frameCount * 0.05) * 0.2;
  ctx.fillStyle = `rgba(255,50,50,${glowAlpha})`;
  ctx.font = 'bold 34px monospace';
  ctx.fillText(titleChars.substring(0, revealed), titleX, CANVAS_H / 2 - 20);
  // Main text
  ctx.fillStyle = '#FFF';
  ctx.font = 'bold 32px monospace';
  ctx.fillText(titleChars.substring(0, revealed), titleX, CANVAS_H / 2 - 20);
  // Stars decoration
  ctx.fillStyle = '#FFD700'; ctx.font = 'bold 18px monospace';
  if (revealed >= titleChars.length) {
    ctx.fillText('\u2605', titleX - 120, CANVAS_H / 2 - 18);
    ctx.fillText('\u2605', titleX + 120, CANVAS_H / 2 - 18);
  }
  // Press enter
  if (stateTimer > 80 && frameCount % 60 < 40) {
    ctx.fillStyle = '#AAA'; ctx.font = '10px monospace';
    ctx.fillText('PRESS ENTER TO START', titleX, CANVAS_H / 2 + 30);
  }

  // Controls panel
  if (stateTimer > 40) {
    const ph = 120;
    const px = 24, py = CANVAS_H - ph - 6;
    const pw = CANVAS_W - 48;
    ctx.fillStyle = 'rgba(10,10,30,0.92)';
    roundRect(ctx, px, py, pw, ph, 6); ctx.fill();
    ctx.strokeStyle = '#FFD700'; ctx.lineWidth = 1.5;
    roundRect(ctx, px, py, pw, ph, 6); ctx.stroke();

    ctx.fillStyle = '#FFD700'; ctx.font = 'bold 10px monospace'; ctx.textAlign = 'center';
    ctx.fillText('- CONTROLS -', CANVAS_W / 2, py + 14);

    // Two columns of key bindings
    ctx.font = 'bold 9px monospace';
    const col1 = px + 16, col1v = px + 120;
    const col2 = px + pw/2 + 16, col2v = px + pw/2 + 120;
    const lh = 13;
    const startY = py + 30;

    const drawRow = (label, val, lx, vx, y) => {
      ctx.fillStyle = '#FFD700'; ctx.textAlign = 'left';
      ctx.fillText(label, lx, y);
      ctx.fillStyle = '#FFF';
      ctx.fillText(val, vx, y);
    };

    drawRow('MOVE',      'Arrows / WASD', col1, col1v, startY);
    drawRow('L.PUNCH',   'U',             col1, col1v, startY + lh);
    drawRow('H.PUNCH',   'I',             col1, col1v, startY + lh*2);
    drawRow('BLOCK',     'O  or  L',      col1, col1v, startY + lh*3);

    drawRow('L.KICK',    'J',             col2, col2v, startY);
    drawRow('H.KICK',    'K',             col2, col2v, startY + lh);
    drawRow('THROW',     'U + J together', col2, col2v, startY + lh*2);
    drawRow('DASH',      'tap >> or <<',   col2, col2v, startY + lh*3);

    // Special moves row — plain English, either direction works
    ctx.font = '8px monospace'; ctx.textAlign = 'center';
    ctx.fillStyle = '#FF8800';
    ctx.fillText('FIREBALL: Down + Left or Right + U/I', CANVAS_W/2 - 105, startY + lh*4 + 2);
    ctx.fillText('UPPERCUT: Left or Right + Down + U/I', CANVAS_W/2 + 105, startY + lh*4 + 2);
    ctx.fillText('SPIN KICK: Down + Left or Right + J/K', CANVAS_W/2 - 105, startY + lh*5 + 2);
    ctx.fillText('SUPER: Down + Left or Right + I (meter)', CANVAS_W/2 + 105, startY + lh*5 + 2);
  }
}

// Character select
let selectCursorX = 0, selectCursorY = 0, selectedChar = -1;

function updateCharacterSelect(dt) {
  if (selectedChar >= 0) {
    // Transition timer
    if (stateTimer > 30) {
      const opponentOrder = buildGauntlet(selectedChar);
      setGameState(GS.VS_SCREEN, { p1Char: selectedChar, opponents: opponentOrder, fightIndex: 0 });
    }
    return;
  }
  // Cursor movement (with repeat guard)
  if (justPressed['ArrowLeft'] || justPressed['a'] || justPressed['A']) { selectCursorX = (selectCursorX + 3) % 4; SFX.cursorMove(); }
  if (justPressed['ArrowRight'] || justPressed['d'] || justPressed['D']) { selectCursorX = (selectCursorX + 1) % 4; SFX.cursorMove(); }
  if (justPressed['ArrowUp'] || justPressed['w'] || justPressed['W']) { selectCursorY = (selectCursorY + 1) % 2; SFX.cursorMove(); }
  if (justPressed['ArrowDown'] || justPressed['s'] || justPressed['S']) { selectCursorY = (selectCursorY + 1) % 2; SFX.cursorMove(); }
  if (justPressed['Enter'] || justPressed[' ']) {
    const idx = selectCursorY * 4 + selectCursorX;
    if (idx === 7) { SFX.cursorError(); }
    else if (idx < 7) { selectedChar = idx; SFX.cursorConfirm(); }
  }
}

function renderCharacterSelect(ctx) {
  ctx.fillStyle = '#0A0A1A'; ctx.fillRect(0, 0, CANVAS_W, CANVAS_H);

  // Title
  ctx.fillStyle = (frameCount % 40 < 20) ? '#FFD700' : '#FFF';
  ctx.font = 'bold 16px monospace'; ctx.textAlign = 'center';
  ctx.fillText('\u2605  HELLO WORLD  \u2605', CANVAS_W / 2, 22);

  // Grid
  const gridX = 30, gridY = 90;
  const tileW = 64, tileH = 64, gap = 8;

  for (let r = 0; r < 2; r++) {
    for (let c = 0; c < 4; c++) {
      const idx = r * 4 + c;
      const tx = gridX + c * (tileW + gap);
      const ty = gridY + r * (tileH + gap);
      const isHover = (c === selectCursorX && r === selectCursorY);
      const isLocked = idx === 7;

      // Tile background
      if (isLocked) {
        ctx.fillStyle = '#1A0000';
        const glow = Math.sin(frameCount * 0.08) * 0.3 + 0.3;
        ctx.strokeStyle = `rgba(255,0,0,${glow})`;
      } else if (idx < 7) {
        ctx.fillStyle = '#111';
        ctx.strokeStyle = isHover ?
          `hsl(0,0%,${50 + Math.sin(frameCount * 0.15) * 30}%)` :
          CHARACTERS[idx].colors.accent;
      } else {
        ctx.fillStyle = '#111'; ctx.strokeStyle = '#333';
      }

      ctx.lineWidth = isHover ? 3 : 1;
      ctx.fillRect(tx, ty, tileW, tileH);
      ctx.strokeRect(tx, ty, tileW, tileH);

      if (isLocked) {
        ctx.fillStyle = '#600'; ctx.font = 'bold 20px monospace'; ctx.textAlign = 'center';
        ctx.fillText('???', tx + tileW/2, ty + tileH/2 + 6);
      } else if (idx < 7) {
        // Mini character sprite
        const ch = CHARACTERS[idx];
        ctx.save();
        ctx.translate(tx + tileW/2, ty + 32 + Math.sin(frameCount * 0.05 + idx) * 2);
        ctx.scale(0.6, 0.6);
        BODY_RENDERERS[idx](ctx, 0, -18, 40, 36, frameCount, FS.IDLE);
        ctx.restore();
        // Name
        ctx.fillStyle = '#FFF'; ctx.font = '6px monospace'; ctx.textAlign = 'center';
        ctx.fillText(ch.name, tx + tileW/2, ty + tileH - 4);
      }

      // Selected flash
      if (selectedChar === idx) {
        const flash = (frameCount % 8 < 4) ? 'rgba(255,255,255,0.6)' : 'transparent';
        ctx.fillStyle = flash; ctx.fillRect(tx, ty, tileW, tileH);
      }
    }
  }

  // Portrait panel (right side)
  const hoveredIdx = selectCursorY * 4 + selectCursorX;
  if (hoveredIdx < 7) {
    const ch = CHARACTERS[hoveredIdx];
    const px = 320, py = 40;
    // Portrait bg
    ctx.fillStyle = '#0D0D1A'; ctx.fillRect(px, py, 140, 180);
    ctx.strokeStyle = ch.colors.accent; ctx.lineWidth = 2; ctx.strokeRect(px, py, 140, 180);

    // Large sprite
    ctx.save();
    ctx.translate(px + 70, py + 80);
    ctx.scale(1.8, 1.8);
    BODY_RENDERERS[hoveredIdx](ctx, 0, -18, 40, 36, frameCount, FS.IDLE);
    ctx.restore();

    // Name
    ctx.fillStyle = '#FFF'; ctx.font = 'bold 12px monospace'; ctx.textAlign = 'center';
    ctx.fillText(ch.name, px + 70, py + 130);

    // Stat bars
    const stats = ch.stars;
    const labels = ['SPD', 'ATK', 'HP'];
    const vals = [stats.spd, stats.atk, stats.hp];
    for (let i = 0; i < 3; i++) {
      const sy = py + 145 + i * 12;
      ctx.fillStyle = '#888'; ctx.font = '6px monospace'; ctx.textAlign = 'left';
      ctx.fillText(labels[i], px + 10, sy + 6);
      ctx.fillStyle = '#333'; ctx.fillRect(px + 35, sy, 80, 6);
      ctx.fillStyle = ch.colors.accent;
      ctx.fillRect(px + 35, sy, vals[i] / 6 * 80, 6);
    }
  }

  // Bottom prompt
  if (selectedChar < 0 && frameCount % 60 < 40) {
    ctx.fillStyle = '#AAA'; ctx.font = '8px monospace'; ctx.textAlign = 'center';
    ctx.fillText('PRESS ENTER TO FIGHT', CANVAS_W / 2, CANVAS_H - 8);
  }
}

function buildGauntlet(playerCharIdx) {
  const order = [...GAUNTLET_ORDER];
  // Remove player's character from gauntlet, replace mirror slot
  const playerInOrder = order.indexOf(playerCharIdx);
  let mirrorChar;
  if (playerInOrder >= 0) {
    // Player is in the gauntlet, find who to put in their slot
    // Use JWX (0) as mirror if player picked someone else, otherwise use next available
    const remaining = [0,1,2,3,4,5,6].filter(i => i !== playerCharIdx && !order.includes(i));
    mirrorChar = remaining.length > 0 ? remaining[0] : playerCharIdx;
    order[playerInOrder] = mirrorChar;
  } else {
    mirrorChar = playerCharIdx; // Mirror fight
  }
  order.push(mirrorChar); // Fight 7: mirror
  order.push(CHAR.HELLO); // Fight 8: boss
  return order;
}

function renderVSScreen(ctx) {
  ctx.fillStyle = '#000'; ctx.fillRect(0, 0, CANVAS_W, CANVAS_H);

  const sd = stateData;
  const p1Char = CHARACTERS[sd.p1Char];
  const opIdx = sd.opponents[sd.fightIndex];
  const p2Char = CHARACTERS[opIdx];

  // P1 side
  ctx.save(); ctx.translate(100, 130); ctx.scale(2, 2);
  BODY_RENDERERS[sd.p1Char](ctx, 0, -18, 40, 36, frameCount, FS.IDLE);
  ctx.restore();
  ctx.fillStyle = '#FFF'; ctx.font = 'bold 12px monospace'; ctx.textAlign = 'center';
  ctx.fillText(p1Char.name, 100, 200);

  // VS
  const vsScale = 1 + Math.sin(frameCount * 0.1) * 0.1;
  ctx.save(); ctx.translate(CANVAS_W/2, 120); ctx.scale(vsScale, vsScale);
  ctx.fillStyle = '#FF0'; ctx.font = 'bold 36px monospace'; ctx.textAlign = 'center';
  ctx.fillText('VS', 0, 0);
  ctx.restore();

  // P2 side
  ctx.save(); ctx.translate(380, 130); ctx.scale(2, 2);
  BODY_RENDERERS[opIdx](ctx, 0, -18, 40, 36, frameCount, FS.IDLE);
  ctx.restore();
  ctx.fillStyle = '#FFF'; ctx.font = 'bold 12px monospace'; ctx.textAlign = 'center';
  ctx.fillText(p2Char.name, 380, 200);

  // Stage name
  const stIdx = Math.min(sd.fightIndex, STAGES.length - 1);
  ctx.fillStyle = '#888'; ctx.font = '8px monospace';
  ctx.fillText(STAGES[stIdx].name, CANVAS_W/2, 240);

  // Fight number
  ctx.fillStyle = '#FFD700'; ctx.font = 'bold 10px monospace';
  ctx.fillText(`FIGHT ${sd.fightIndex + 1}`, CANVAS_W/2, 30);
}

function renderGameOver(ctx) {
  ctx.fillStyle = '#000'; ctx.fillRect(0, 0, CANVAS_W, CANVAS_H);
  ctx.fillStyle = '#FF0000'; ctx.font = 'bold 30px monospace'; ctx.textAlign = 'center';
  ctx.fillText('GAME OVER', CANVAS_W/2, CANVAS_H/2 - 10);
  if (frameCount % 60 < 40) {
    ctx.fillStyle = '#888'; ctx.font = '10px monospace';
    ctx.fillText('PRESS ENTER TO CONTINUE', CANVAS_W/2, CANVAS_H/2 + 30);
  }
}

function renderEnding(ctx) {
  ctx.fillStyle = '#000'; ctx.fillRect(0, 0, CANVAS_W, CANVAS_H);
  const lines = ['> SYSTEM ONLINE', '> RUNNING HELLO_WORLD.EXE', '> ...', '> HELLO WORLD'];
  const charDelay = 4; // frames per character
  const lineDelay = 20; // extra frames between lines
  let charsSoFar = 0;
  let totalFrames = 0;
  ctx.fillStyle = '#00FF44'; ctx.font = '12px monospace'; ctx.textAlign = 'left';
  for (let i = 0; i < lines.length; i++) {
    const lineStart = totalFrames;
    const lineLen = lines[i].length;
    const charsRevealed = Math.min(lineLen, Math.max(0, Math.floor((stateTimer - lineStart) / charDelay)));
    if (charsRevealed > 0) {
      ctx.fillText(lines[i].substring(0, charsRevealed), 40, 80 + i * 30);
    }
    totalFrames += lineLen * charDelay + lineDelay;
    if (i === lines.length - 1 && charsRevealed >= lineLen) {
      // Cursor blink
      if (frameCount % 40 < 20) {
        ctx.fillText('_', 40 + charsRevealed * 7.2, 80 + i * 30);
      }
      // JWXAIPOC branding
      if (stateTimer > totalFrames + 60) {
        ctx.fillStyle = '#FFF'; ctx.font = '8px monospace'; ctx.textAlign = 'right';
        ctx.fillText('POWERED BY JWXAIPOC', CANVAS_W - 20, 40);
      }
      // Play again
      if (stateTimer > totalFrames + 120 && frameCount % 60 < 40) {
        ctx.fillStyle = '#00FF44'; ctx.font = '10px monospace'; ctx.textAlign = 'center';
        ctx.fillText('PLAY AGAIN? [ENTER]', CANVAS_W/2, CANVAS_H - 30);
      }
    }
  }
}

// Boss intro cinematic
function renderBossIntro(ctx) {
  ctx.fillStyle = '#000'; ctx.fillRect(0, 0, CANVAS_W, CANVAS_H);
  const t = stateTimer;

  if (t < 30) {
    // Blinking cursor
    if (frameCount % 30 < 15) {
      ctx.fillStyle = '#00FF44'; ctx.font = '12px monospace'; ctx.textAlign = 'center';
      ctx.fillText('>', CANVAS_W/2, CANVAS_H/2);
    }
  } else if (t < 80) {
    // INITIALIZING...
    const text = '> INITIALIZING...';
    const chars = Math.min(text.length, Math.floor((t - 30) / 3));
    ctx.fillStyle = '#00FF44'; ctx.font = '12px monospace'; ctx.textAlign = 'center';
    ctx.fillText(text.substring(0, chars), CANVAS_W/2, CANVAS_H/2);
  } else if (t < 140) {
    // Globe arena fading in
    const alpha = (t - 80) / 60;
    ctx.globalAlpha = alpha;
    drawStageFar(ctx, 7);
    ctx.globalAlpha = 1;
  } else if (t < 200) {
    // HELLO drops in
    drawStageBackground(ctx, 7, 0);
    const dropY = Math.min(PHYSICS.GROUND_Y, -50 + (t - 140) * 5);
    ctx.save(); ctx.translate(CANVAS_W/2, dropY - 36);
    const s = 1.5;
    ctx.scale(s, s);
    drawHELLOBody(ctx, 0, -36, 48, 48, frameCount, FS.IDLE, 1);
    ctx.restore();
    if (t === 180) triggerShake(3, 10);
  } else if (t < 260) {
    // H E L L O letters
    drawStageBackground(ctx, 7, 0);
    ctx.save(); ctx.translate(CANVAS_W/2, PHYSICS.GROUND_Y - 60);
    drawHELLOBody(ctx, 0, -36, 48, 48, frameCount, FS.IDLE, 1);
    ctx.restore();
    const letters = 'HELLO';
    const revealed = Math.min(letters.length, Math.floor((t - 200) / 10));
    ctx.fillStyle = '#FFF'; ctx.font = 'bold 24px monospace'; ctx.textAlign = 'center';
    let helloText = '';
    for (let i = 0; i < revealed; i++) helloText += letters[i] + ' ';
    ctx.fillText(helloText.trim(), CANVAS_W/2, PHYSICS.GROUND_Y + 20);
  } else {
    // Flash and transition
    if (t < 265) { ctx.fillStyle = '#FFF'; ctx.fillRect(0, 0, CANVAS_W, CANVAS_H); }
    else { startFight(); }
  }
}

// Flavor text between fights
const FLAVOR_TEXT = {
  0: 'The gauntlet begins. Your rivals await.',
  3: 'Something stirs beyond the network...',
  5: 'The data paths converge. Something is watching.',
  6: 'One last echo before the storm.',
};


// ═══════════════════════════════════════════
// SECTION 13: GAME STATE MACHINE & COLLISION
// ═══════════════════════════════════════════

let gameState = GS.TITLE_SCREEN;
let stateTimer = 0;
let stateData = {};
let frameCount = 0;
let player1 = null, player2 = null;
let camera = { x: 0 };
let roundTimer = 90;
let currentRound = 1;
let currentFightIndex = 0;
let debugMode = false;
let superFreezeTimer = 0;
let helloTeaseTimer = 0;
let helloTeaseType = 0;

function setGameState(newState, data) {
  stopMusic(0.5);
  particles.length = 0;
  floatingDamage.length = 0;
  announcementText = '';
  announcementTimer = 0;
  gameState = newState;
  stateTimer = 0;
  stateData = data || stateData;

  switch (newState) {
    case GS.TITLE_SCREEN:
      selectedChar = -1;
      playTrack(TRACK_TITLE);
      break;
    case GS.CHARACTER_SELECT:
      selectCursorX = 0; selectCursorY = 0; selectedChar = -1;
      playTrack(TRACK_SELECT);
      break;
    case GS.VS_SCREEN:
      break;
    case GS.ROUND_INTRO:
      showAnnouncement(`ROUND ${currentRound}`, '#FFF', 60);
      break;
    case GS.FIGHTING: {
      const stIdx = Math.min(stateData.fightIndex, STAGES.length - 1);
      playTrack(STAGE_TRACKS[stIdx]);
      resetAmbientParticles(stIdx);
      break;
    }
    case GS.BOSS_INTRO:
      break;
    case GS.GAME_OVER:
      playTrack(TRACK_GAMEOVER, false);
      break;
    case GS.ENDING:
      playTrack(TRACK_ENDING, false);
      break;
  }
}

function startFight() {
  const sd = stateData;
  const opIdx = sd.opponents[sd.fightIndex];
  player1 = new Fighter(sd.p1Char, 0, 200);
  player2 = new Fighter(opIdx, 1, 760);
  roundTimer = 90;
  currentRound = 1;
  currentFightIndex = sd.fightIndex;
  camera.x = (player1.x + player2.x) / 2 - CANVAS_W / 2;
  const stIdx = Math.min(sd.fightIndex, STAGES.length - 1);
  resetAmbientParticles(stIdx);
  setGameState(GS.ROUND_INTRO);
}

function processPlayerInput(fighter) {
  if (!fighter.isActionable() && !fighter.canCancel()) return;

  // Special move detection first
  const special = detectSpecialMove();
  if (special) {
    if (special === SPECIAL.SUPER && fighter.superMeter >= 100) {
      fighter.setState(FS.ATK_SUPER);
      fighter.superMeter = 0;
      superFreezeTimer = 8;
      SFX.superActivate();
      return;
    }
    if (special === SPECIAL.FIREBALL && !projectiles.some(p => p.owner === fighter)) {
      fighter.setState(FS.ATK_SPECIAL);
      fighter.specialType = SPECIAL.FIREBALL;
      const dir = fighter.facingRight ? 1 : -1;
      const ch = CHARACTERS[fighter.charIndex];
      projectiles.push(new Projectile(fighter, fighter.x + dir * 30, fighter.y - 30, dir * 280, 0, 10, ch.projectileColor, ch.projectileShape));
      SFX.fireballLaunch();
      return;
    }
    if (special === SPECIAL.DP) {
      fighter.setState(FS.ATK_SPECIAL);
      fighter.specialType = SPECIAL.DP;
      fighter.vy = PHYSICS.JUMP_VELOCITY * 0.8;
      fighter.vx = (fighter.facingRight ? 1 : -1) * 120;
      fighter.onGround = false;
      SFX.specialActivate();
      return;
    }
    if (special === SPECIAL.SPIN_KICK) {
      fighter.setState(FS.ATK_SPECIAL);
      fighter.specialType = SPECIAL.SPIN_KICK;
      fighter.vx = (fighter.facingRight ? 1 : -1) * 200;
      SFX.specialActivate();
      return;
    }
  }

  // Dash — works on ground and in the air, absolute direction
  const dash = checkDash();
  if (dash && fighter.state !== FS.DASHING) {
    fighter.setState(FS.DASHING);
    fighter.dashDir = dash;
    fighter.dashTimer = PHYSICS.DASH_DURATION;
    return;
  }

  const cur = inputBuffer.length > 0 ? inputBuffer[inputBuffer.length - 1] : null;
  if (!cur) return;

  // Throw (LP + LK simultaneous)
  if (cur.buttons.has('LP') && cur.buttons.has('LK')) {
    fighter.setState(FS.THROW);
    return;
  }

  // Attacks
  if (cur.buttons.has('LP')) {
    if (!fighter.onGround) fighter.setState(FS.ATK_AIR_LP);
    else if (cur.dirs.has('D')) fighter.setState(FS.ATK_CROUCH_LP);
    else fighter.setState(FS.ATK_LP);
    return;
  }
  if (cur.buttons.has('HP')) {
    fighter.setState(FS.ATK_HP);
    return;
  }
  if (cur.buttons.has('LK')) {
    if (!fighter.onGround) fighter.setState(FS.ATK_AIR_HK);
    else fighter.setState(FS.ATK_LK);
    return;
  }
  if (cur.buttons.has('HK')) {
    if (cur.dirs.has('D')) fighter.setState(FS.ATK_CROUCH_HK);
    else fighter.setState(FS.ATK_HK);
    return;
  }

  // Block
  if (cur.buttons.has('BL')) {
    if (cur.dirs.has('D')) fighter.setState(FS.CROUCH_BLOCKING);
    else fighter.setState(FS.BLOCKING);
    return;
  }

  // Movement
  if (cur.dirs.has('U') && fighter.onGround) {
    fighter.setState(FS.JUMPING);
    fighter.vy = PHYSICS.JUMP_VELOCITY;
    fighter.onGround = false;
    if (cur.dirs.has('R')) fighter.vx = PHYSICS.WALK_SPEED * fighter.speed;
    if (cur.dirs.has('L')) fighter.vx = -PHYSICS.WALK_SPEED * fighter.speed;
    SFX.jump();
    return;
  }
  if (cur.dirs.has('D') && fighter.onGround) {
    fighter.setState(FS.CROUCHING);
    return;
  }
  if ((cur.dirs.has('L') || cur.dirs.has('R')) && fighter.onGround) {
    fighter.setState(FS.WALKING);
    return;
  }
  if (fighter.state === FS.WALKING && fighter.onGround) {
    fighter.setState(FS.IDLE);
  }
}

function checkHitCollisions(attacker, defender) {
  const hitbox = attacker.getHitbox();
  if (!hitbox) return;
  const hurtbox = defender.getHurtbox();
  if (!aabbOverlap(hitbox, hurtbox)) return;

  // Check block
  const isBlocking = defender.state === FS.BLOCKING || defender.state === FS.CROUCH_BLOCKING;
  // Check parry
  const isParry = defender.parryWindow > 0 && isBlocking;

  if (isParry) {
    // Perfect parry
    attacker.setState(FS.HIT_STUN);
    attacker.stateFrame = -8; // brief stun
    defender.superMeter = Math.min(100, defender.superMeter + 15);
    SFX.parry();
    spawnBurst(defender.x, defender.y - 20, 5, 100, 0.3, 2, '#FFF');
  } else if (isBlocking) {
    // Chip damage
    const chip = Math.round(hitbox.damage * 0.1);
    defender.takeChipDamage(chip);
    defender.superMeter = Math.max(0, defender.superMeter - 5);
    attacker.superMeter = Math.min(100, attacker.superMeter + 2);
    SFX.block();
    spawnBurst(defender.x + (attacker.x < defender.x ? -15 : 15), defender.y - 25, 3, 80, 0.2, 2, '#AAF');
  } else {
    // Full hit
    const comboScaling = Math.max(0.2, 1 - (attacker.comboCount * 0.1));
    const dmg = defender.takeHit(hitbox, attacker.x, comboScaling);
    attacker.superMeter = Math.min(100, attacker.superMeter + 5);
    attacker.comboCount++;
    attacker.lastHitFrame = frameCount;

    // SFX
    if (hitbox.type === 'punch') { hitbox.damage > 10 ? SFX.punchHeavy() : SFX.punchLight(); }
    else if (hitbox.type === 'kick') { hitbox.damage > 10 ? SFX.kickHeavy() : SFX.kickLight(); }
    else if (hitbox.type === 'throw') { SFX.throwHit(); }
    else { SFX.punchHeavy(); }

    // Particles
    const hx = (hitbox.x + hitbox.w/2), hy = (hitbox.y + hitbox.h/2);
    spawnBurst(hx, hy, 6, 120, 0.3, 3, CHARACTERS[attacker.charIndex].colors.accent);

    // Floating damage
    floatingDamage.push({ x: defender.x, y: defender.y - 50, amount: dmg, life: 30, color: attacker.playerIndex === 0 ? '#FF4444' : '#4444FF' });

    // Combo SFX
    if (attacker.comboCount >= 2) SFX.comboHit(attacker.comboCount);
  }
  attacker.hasHit = true;
}

function checkProjectileCollisions() {
  for (let i = projectiles.length - 1; i >= 0; i--) {
    const proj = projectiles[i];
    if (proj.dead || proj.hasHit) continue;

    // vs fighters
    const targets = [player1, player2].filter(f => f !== proj.owner);
    for (const target of targets) {
      if (target.barrier > 0) { proj.dead = true; spawnBurst(proj.x, proj.y, 4, 80, 0.2, 2, '#FFF'); break; }
      const hurtbox = target.getHurtbox();
      if (aabbOverlap(proj.getHitbox(), hurtbox)) {
        const isBlocking = target.state === FS.BLOCKING || target.state === FS.CROUCH_BLOCKING;
        if (isBlocking) {
          target.takeChipDamage(Math.round(proj.damage * 0.1));
          SFX.block();
        } else {
          target.takeHit({ x: proj.x, y: proj.y, w: proj.w, h: proj.h, damage: proj.damage, stun: 15, knockbackX: proj.vx > 0 ? 100 : -100, knockbackY: -30, type: 'projectile', knockdown: false }, proj.x, 1);
          SFX.fireballHit();
        }
        spawnBurst(proj.x, proj.y, 5, 100, 0.3, 3, proj.color);
        proj.dead = true;
        break;
      }
    }

    // vs other projectiles
    if (!proj.dead) {
      for (let j = i - 1; j >= 0; j--) {
        const other = projectiles[j];
        if (other.dead || other.owner === proj.owner) continue;
        if (aabbOverlap(proj.getHitbox(), other.getHitbox())) {
          proj.dead = true; other.dead = true;
          spawnBurst((proj.x + other.x)/2, (proj.y + other.y)/2, 8, 100, 0.3, 2, '#FFF');
        }
      }
    }
  }
}

function handleRoundEnd(winner) {
  winner.roundsWon++;
  if (winner.hp === winner.maxHp) showAnnouncement('PERFECT!', '#FFD700', 80);
  else if (roundTimer <= 0) showAnnouncement('TIME OUT', '#FF8800', 60);
  else showAnnouncement('KO!', '#FF2222', 80);
  SFX.ko();

  setGameState(GS.ROUND_END);
  stateData.winner = winner === player1 ? 0 : 1;
}

function handleTimeout() {
  if (player1.hp > player2.hp) handleRoundEnd(player1);
  else if (player2.hp > player1.hp) handleRoundEnd(player2);
  else {
    showAnnouncement('DRAW', '#FFF', 60);
    setGameState(GS.ROUND_END);
    stateData.winner = -1;
  }
}


// ═══════════════════════════════════════════
// SECTION 14: GAME LOOP
// ═══════════════════════════════════════════

const canvas = document.getElementById('gameCanvas');
const ctx = canvas.getContext('2d');

function resizeCanvas() {
  const scaleX = window.innerWidth / CANVAS_W;
  const scaleY = window.innerHeight / CANVAS_H;
  const scale = Math.min(scaleX, scaleY);
  canvas.style.width = (CANVAS_W * scale) + 'px';
  canvas.style.height = (CANVAS_H * scale) + 'px';
}
window.addEventListener('resize', resizeCanvas);
resizeCanvas();

let lastTimestamp = 0;

function gameLoop(timestamp) {
  const dt = Math.min((timestamp - lastTimestamp) / 1000, 1/30);
  lastTimestamp = timestamp;
  frameCount++;
  stateTimer++;
  updateShake();

  // Debug toggle
  if (justPressed['F1']) debugMode = !debugMode;

  // Super freeze
  if (superFreezeTimer > 0) {
    superFreezeTimer--;
    ctx.fillStyle = `rgba(255,255,255,${superFreezeTimer / 8 * 0.3})`;
    ctx.fillRect(0, 0, CANVAS_W, CANVAS_H);
    sampleInput(frameCount);
    requestAnimationFrame(gameLoop);
    return;
  }

  // Update
  switch (gameState) {
    case GS.TITLE_SCREEN:
      updateTitleScreen(dt);
      break;
    case GS.CHARACTER_SELECT:
      updateCharacterSelect(dt);
      break;
    case GS.VS_SCREEN:
      if (stateTimer > 90) {
        const sd = stateData;
        if (sd.fightIndex === sd.opponents.length - 1) {
          // Boss fight
          setGameState(GS.BOSS_INTRO);
        } else {
          startFight();
        }
      }
      break;
    case GS.ROUND_INTRO:
      // Drain input so stale keys don't trigger on fight start
      justPressed = {};
      inputBuffer.length = 0;
      if (stateTimer === 60) showAnnouncement('FIGHT!', '#FFD700', 40);
      if (stateTimer > 100) setGameState(GS.FIGHTING);
      break;
    case GS.FIGHTING:
      sampleInput(frameCount);
      if (player1 && player2) {
        // Update camera FIRST so screen-relative boundaries work
        const stIdx = Math.min(stateData.fightIndex, STAGES.length - 1);
        if (stIdx === 7) { camera.x = 0; } // Globe arena fixed
        else {
          camera.x = (player1.x + player2.x) / 2 - CANVAS_W / 2;
          camera.x = clamp(camera.x, 0, STAGE_WIDTH - CANVAS_W);
        }

        processPlayerInput(player1);
        // AI
        if (player2.charIndex === CHAR.HELLO) updateHelloAI(player2, player1, frameCount);
        else updateAI(player2, player1, frameCount);

        player1.update(dt, frameCount, player2);
        player2.update(dt, frameCount, player1);

        // Projectiles
        for (let i = projectiles.length - 1; i >= 0; i--) {
          projectiles[i].update(dt);
          if (projectiles[i].dead) projectiles.splice(i, 1);
        }

        // Collisions
        checkHitCollisions(player1, player2);
        checkHitCollisions(player2, player1);
        checkProjectileCollisions();

        // Particles
        updateParticles(dt);
        updateAmbientParticles(dt, Math.min(stateData.fightIndex, STAGES.length - 1));

        // Timer
        roundTimer -= dt;
        if (roundTimer <= 0) { roundTimer = 0; handleTimeout(); }

        // KO check
        if (player1.hp <= 0 && gameState === GS.FIGHTING) handleRoundEnd(player2);
        else if (player2.hp <= 0 && gameState === GS.FIGHTING) handleRoundEnd(player1);

        // HELLO tease
        if (stateData.fightIndex >= 3 && stateData.fightIndex <= 6) {
          if (helloTeaseTimer > 0) helloTeaseTimer--;
        }
      }
      break;
    case GS.ROUND_END:
      if (stateTimer > 120) {
        // Check match end
        const p1Wins = player1.roundsWon >= 2;
        const p2Wins = player2.roundsWon >= 2;
        if (p1Wins || p2Wins) {
          setGameState(GS.MATCH_END);
          stateData.matchWinner = p1Wins ? 0 : 1;
        } else {
          // Next round — full reset of HP and positions
          currentRound++;
          for (const f of [player1, player2]) {
            f.hp = f.maxHp;
            f.ghostHp = f.maxHp;
            f.displayedHp = f.maxHp;
            f.ghostHpDelay = 0;
            f.setState(FS.IDLE);
            f.vx = 0; f.vy = 0;
            f.y = PHYSICS.GROUND_Y;
            f.onGround = true;
            f.comboCount = 0;
            f.hitFlash = 0;
            f.invisible = 0;
            f.powerUp = 0;
            f.barrier = 0;
          }
          player1.x = 200; player2.x = 760;
          player1.facingRight = true; player2.facingRight = false;
          roundTimer = 90;
          projectiles.length = 0;
          particles.length = 0;
          inputBuffer.length = 0;
          justPressed = {};
          setGameState(GS.ROUND_INTRO);
        }
      }
      break;
    case GS.MATCH_END:
      if (stateTimer === 1) {
        if (stateData.matchWinner === 0) {
          showAnnouncement('YOU WIN!', '#FFD700', 120);
          playTrack(TRACK_VICTORY, false);
          // HELLO tease on fights 4-7
          if (stateData.fightIndex >= 3 && stateData.fightIndex <= 5) {
            helloTeaseTimer = 30; helloTeaseType = stateData.fightIndex;
          }
          if (stateData.fightIndex === 6) {
            // Fight 7 - HELLO reveal
            helloTeaseTimer = 120; helloTeaseType = 6;
          }
        } else {
          showAnnouncement('YOU LOSE', '#FF2222', 80);
        }
      }
      if (stateTimer > 150) {
        if (stateData.matchWinner === 1) {
          setGameState(GS.GAME_OVER);
        } else {
          // Next opponent
          stateData.fightIndex++;
          if (stateData.fightIndex >= stateData.opponents.length) {
            setGameState(GS.ENDING);
          } else {
            setGameState(GS.VS_SCREEN);
          }
        }
      }
      break;
    case GS.BOSS_INTRO:
      // Handled in render
      if (stateTimer > 265) startFight();
      break;
    case GS.GAME_OVER:
      if (justPressed['Enter'] || justPressed[' ']) {
        setGameState(GS.TITLE_SCREEN);
      }
      break;
    case GS.ENDING:
      if (stateTimer > 400 && (justPressed['Enter'] || justPressed[' '])) {
        setGameState(GS.TITLE_SCREEN);
      }
      break;
  }

  sampleInput(frameCount);

  // ── Render ──
  ctx.clearRect(0, 0, CANVAS_W, CANVAS_H);
  ctx.save();
  ctx.translate(shakeX, shakeY);

  switch (gameState) {
    case GS.TITLE_SCREEN:
      renderTitleScreen(ctx);
      break;
    case GS.CHARACTER_SELECT:
      renderCharacterSelect(ctx);
      break;
    case GS.VS_SCREEN:
      renderVSScreen(ctx);
      break;
    case GS.ROUND_INTRO:
    case GS.FIGHTING:
    case GS.ROUND_END:
    case GS.MATCH_END: {
      const stIdx = Math.min(stateData.fightIndex || 0, STAGES.length - 1);
      drawStageBackground(ctx, stIdx, camera.x);
      // Draw fighters
      if (player1) drawCharacter(ctx, player1, camera.x);
      if (player2) drawCharacter(ctx, player2, camera.x);
      // Projectiles
      for (const p of projectiles) p.draw(ctx, camera.x);
      // Particles
      renderParticles(ctx, camera.x);
      // HUD
      if (player1 && player2) drawHUD(ctx, player1, player2, roundTimer, currentRound);

      // HELLO tease overlay
      if (helloTeaseTimer > 0 && gameState === GS.MATCH_END) {
        if (helloTeaseType <= 5) {
          // Subtle globe silhouette
          ctx.globalAlpha = 0.08;
          ctx.fillStyle = '#1A6EBD'; ctx.beginPath();
          ctx.arc(CANVAS_W/2, CANVAS_H/2, 60, 0, Math.PI*2); ctx.fill();
          ctx.globalAlpha = 1;
        } else if (helloTeaseType === 6 && helloTeaseTimer > 30) {
          // Full HELLO reveal
          ctx.fillStyle = 'rgba(0,0,0,0.8)'; ctx.fillRect(0, 0, CANVAS_W, CANVAS_H);
          ctx.save(); ctx.translate(CANVAS_W/2, CANVAS_H/2);
          ctx.scale(2, 2);
          ctx.globalAlpha = 0.8;
          drawHELLOBody(ctx, 0, -36, 48, 48, frameCount, FS.IDLE, 1);
          ctx.globalAlpha = 1;
          ctx.restore();
        }
      }

      // Debug mode
      if (debugMode && player1 && player2) {
        ctx.globalAlpha = 0.4;
        // Hitboxes
        for (const f of [player1, player2]) {
          const hb = f.getHitbox();
          if (hb) { ctx.fillStyle = 'rgba(255,0,0,0.4)'; ctx.fillRect(hb.x - camera.x, hb.y, hb.w, hb.h); }
          const ub = f.getHurtbox();
          ctx.fillStyle = 'rgba(0,0,255,0.3)'; ctx.fillRect(ub.x - camera.x, ub.y, ub.w, ub.h);
          // State label
          ctx.globalAlpha = 1;
          ctx.fillStyle = '#FFF'; ctx.font = '6px monospace'; ctx.textAlign = 'center';
          ctx.fillText(f.state, f.x - camera.x, f.y - 65);
        }
        // Boundaries
        ctx.strokeStyle = '#FF0'; ctx.lineWidth = 1;
        ctx.beginPath(); ctx.moveTo(PHYSICS.LEFT_BOUNDARY - camera.x, 0); ctx.lineTo(PHYSICS.LEFT_BOUNDARY - camera.x, CANVAS_H); ctx.stroke();
        ctx.beginPath(); ctx.moveTo(PHYSICS.RIGHT_BOUNDARY - camera.x, 0); ctx.lineTo(PHYSICS.RIGHT_BOUNDARY - camera.x, CANVAS_H); ctx.stroke();
        // Frame counter
        ctx.fillStyle = '#FF0'; ctx.font = '6px monospace'; ctx.textAlign = 'right';
        ctx.fillText(`F:${frameCount}`, CANVAS_W - 5, 10);
        ctx.globalAlpha = 1;
      }
      break;
    }
    case GS.BOSS_INTRO:
      renderBossIntro(ctx);
      break;
    case GS.GAME_OVER:
      renderGameOver(ctx);
      break;
    case GS.ENDING:
      renderEnding(ctx);
      break;
  }

  ctx.restore();
  requestAnimationFrame(gameLoop);
}

// Start
requestAnimationFrame(gameLoop);

</script>
</body>
</html>
