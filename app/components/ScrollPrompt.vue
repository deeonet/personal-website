<template>
    <div
      :class="['scroll-prompt', `position-${position}`]"
      role="button"
      :aria-label="ariaLabel"
      tabindex="0"
      @click="handleClick"
      @keydown.space.prevent="handleClick"
      @keydown.enter.prevent="handleClick"
    >
      <div class="ring" aria-hidden="true"></div>
  
      <!-- SVG arrow inside a rounded capsule -->
      <svg
        class="arrow"
        :width="size"
        :height="size"
        viewBox="0 0 48 48"
        xmlns="http://www.w3.org/2000/svg"
        aria-hidden="true"
        focusable="false"
      >
        <g transform="translate(24, 24)">
          <!-- capsule / container circle -->
          <rect x="-14" y="-18" width="28" height="36" rx="14" fill="none" stroke="none"/>
          <!-- arrow shaft -->
          <path
            class="arrow-shaft"
            d="M0 -6 V6"
            stroke="currentColor"
            stroke-width="2.5"
            stroke-linecap="round"
            stroke-linejoin="round"
            fill="none"
          />
          <!-- arrow head -->
          <path
            class="arrow-head"
            d="M-5 0 L0 6 L5 0"
            stroke="currentColor"
            stroke-width="2.5"
            stroke-linecap="round"
            stroke-linejoin="round"
            fill="none"
          />
        </g>
      </svg>
  
      <span v-if="label" class="label">{{ label }}</span>
    </div>
  </template>
  
  <script setup>
  import { computed } from 'vue'
  
  /**
   * Props
   * - target: CSS selector to scroll to when clicked. If empty, calls window.scrollBy(...)
   * - label: optional visible text under the icon (e.g. "Scroll")
   * - position: 'center' | 'left' | 'right' (on desktop). Also supports 'fixed' for custom use.
   * - size: pixel size of the SVG (defaults to 44)
   * - color: CSS color for the icon (defaults to currentColor — set via parent)
   */
  const props = defineProps({
    target: { type: String, default: '' },
    label: { type: String, default: '' },
    position: { type: String, default: 'center' },
    size: { type: [Number, String], default: 44 },
    color: { type: String, default: '' },
    ariaLabel: { type: String, default: 'Scroll down' }
  })
  
  const handleClick = (e) => {
    // If a target selector is provided, smooth scroll to it
    if (props.target) {
      const el = document.querySelector(props.target)
      if (el && typeof el.scrollIntoView === 'function') {
        el.scrollIntoView({ behavior: 'smooth', block: 'start' })
        return
      }
    }
  
    // fallback: scroll down by viewport height
    window.scrollBy({ top: window.innerHeight * 0.85, behavior: 'smooth' })
  }
  </script>
  
  <style scoped>
  /* Layout & placement */
  .scroll-prompt {
    display: inline-flex;
    flex-direction: column;
    align-items: center;
    gap: 8px;
    cursor: pointer;
    user-select: none;
    color: #0f172a; /* default color, can be overriden via color prop or parent */
    --prompt-size: 44px;
    --ring-size: 64px;
    transition: transform .18s ease;
    outline: none;
  }
  
  /* Accept numeric prop for size via attribute (inline styles not used here because this file is scoped).
     You can override with inline style: <ScrollPrompt style="--prompt-size:56px"> */
  .arrow {
    width: var(--prompt-size);
    height: var(--prompt-size);
    display: block;
    overflow: visible;
  }
  
  /* Subtle hover lift */
  .scroll-prompt:active { transform: translateY(2px); }
  .scroll-prompt:focus { box-shadow: 0 6px 20px rgba(15,23,42,0.08); border-radius: 9999px; }
  
  /* Label */
  .label {
    font-size: 13px;
    color: rgba(15,23,42,0.8);
    letter-spacing: 0.02em;
  }
  
  /* Pulse ring behind the icon */
  .ring {
    position: absolute;
    width: var(--ring-size);
    height: var(--ring-size);
    border-radius: 9999px;
    background: radial-gradient(circle at center, rgba(99,102,241,0.12) 0%, rgba(99,102,241,0.04) 35%, transparent 60%);
    z-index: -1;
    filter: blur(6px);
    transform-origin: center;
    pointer-events: none;
    animation: ringPulse 2200ms ease-in-out infinite;
    opacity: 0.95;
  }
  
  /* Position variations */
  .position-center { position: relative; margin: 0 auto; }
  .position-left { position: relative; margin-right: auto; }
  .position-right { position: relative; margin-left: auto; }
  
  /* Arrow animation:
     - The shaft is animated with a vertical translate to give a "down" motion.
     - The arrow head gently bounces and fades-in/out for motion cues.
  */
  @keyframes arrowBounce {
    0%   { transform: translateY(-2px); opacity: 0.9; }
    40%  { transform: translateY(6px); opacity: 1; }
    70%  { transform: translateY(2px); opacity: 0.96; }
    100% { transform: translateY(-2px); opacity: 0.9; }
  }
  
  @keyframes headPop {
    0%   { transform: translateY(-6px) scale(0.98); opacity: 0.0; }
    30%  { transform: translateY(0px) scale(1.02); opacity: 1; }
    60%  { transform: translateY(6px) scale(0.98); opacity: 0.9; }
    100% { transform: translateY(0px) scale(1); opacity: 0.95; }
  }
  
  @keyframes ringPulse {
    0%   { transform: scale(0.9); opacity: 0.35; }
    50%  { transform: scale(1.06); opacity: 0.18; }
    100% { transform: scale(0.9); opacity: 0.35; }
  }
  
  /* Apply animations to SVG parts */
  .arrow-shaft {
    transform-origin: center;
    animation: arrowBounce 1.6s cubic-bezier(.2,.9,.3,1) infinite;
  }
  
  .arrow-head {
    transform-origin: center;
    animation: headPop 1.6s cubic-bezier(.2,.9,.3,1) infinite;
  }
  
  /* Subtle color & sizing control using CSS variables */
  :root {
    --scrollprompt-accent: #6366F1; /* indigo-500 */
  }
  
  /* Use the color prop if present — parent can set --scrollprompt-accent */
  .scroll-prompt { color: var(--scrollprompt-accent); }
  
  /* Respect reduced motion */
  @media (prefers-reduced-motion: reduce) {
    .ring, .arrow-shaft, .arrow-head { animation: none !important; }
  }
  
  /* Small-screen placement helper */
  @media (max-width: 640px) {
    .label { display: none; }
    .ring { display: none; }
    .scroll-prompt { --prompt-size: 40px; --ring-size: 54px; }
  }
  
  /* When the component is focused by keyboard, show a clear focus ring */
  .scroll-prompt:focus {
    box-shadow: 0 0 0 4px rgba(99,102,241,0.12);
    border-radius: 9999px;
  }
  </style>
  