# NEET 2025 Countdown (Conky)

This is a simple Conky configuration that shows:

- Days left until **NEET 2025** (4th May 2025)
- A dynamic countdown display
- A percentage-based progress bar (from 6th May 2024 to 3rd May 2025)

## Features

- Countdown text: Days left / Exam over
- Real-time progress percentage
- Visual progress bar
- Minimal design with custom font and emoji support

## Installation

### Debian/Ubuntu-based:
```bash
sudo apt update
sudo apt install conky-all fonts-ubuntu fonts-noto-color-emoji
```

### Arch-based (Manjaro/EndeavourOS etc.):
```bash
sudo pacman -S conky noto-fonts-emoji ttf-ubuntu-font-family
```

## Setup

1. Create the config directory if it doesn't exist:
```bash
mkdir -p ~/.config/conky
```

2. Create a new file named `neet_countdown.lua`:
```bash
nano ~/.config/conky/neet_countdown.lua
```

3. Paste the following config into the file:

```lua
conky.config = {
    alignment = 'top_left',
    background = false,
    border_width = 0,
    cpu_avg_samples = 2,
    default_color = 'white',
    double_buffer = true,
    font = 'Ubuntu, Noto Color Emoji:bold:size=18',
    gap_x = 50,
    gap_y = 60,
    minimum_width = 280,
    minimum_height = 280,
    no_buffers = true,
    own_window = true,
    own_window_type = 'normal',
    own_window_transparent = false,
    own_window_hints = 'undecorated,below,sticky,skip_taskbar,skip_pager',
    own_window_argb_visual = true,
    own_window_argb_value = 100,
    own_window_colour = '000000',
    own_window_class = 'Conky',
    draw_borders = false,
    draw_graph_borders = false,
    draw_outline = false,
    draw_shades = false,
    update_interval = 1,
    use_xft = true,
    border_inner_margin = 10,
    border_outer_margin = 0,
    border_width = 0,
    draw_shadows = true,
    default_shade_color = '000000'
}

conky.text = [[
${alignc}${color white}${font Ubuntu:bold:size=26}NEET 2025${font}
${voffset -15}
${alignc}${color white}${font Ubuntu:bold:size=60}${if_match ${exec expr $(date -d '2025-05-03' +%s) - $(date +%s)} <= 0}EXAM OVER!${else}${exec expr \( $(date -d '2025-05-03' +%s) - $(date +%s) \) / 86400}${endif}${font}
${voffset -20}
${alignc}${color white}${font Ubuntu:bold:size=24}${if_match ${exec expr $(date -d '2025-05-03' +%s) - $(date +%s)} <= 0}GOOD LUCK!${else}DAYS LEFT${endif}${font}
${voffset -15}
${alignc}${color white}${font Ubuntu:bold:size=18}4TH MAY 2025${font}
${voffset -25}
${alignc}${color white}${font Ubuntu:bold:size=13}PROGRESS: ${exec expr 100 \* \( $(date +%s) - $(date -d '2024-05-06' +%s) \) / \( $(date -d '2025-05-03' +%s) - $(date -d '2024-05-06' +%s) \)}%${font}
${voffset -15}
${color white}${execbar expr \( $(date +%s) - $(date -d '2024-05-06' +%s) \) \* 100 / \( $(date -d '2025-05-03' +%s) - $(date -d '2024-05-06' +%s) \)}
]]
```

4. Run Conky:
```bash
conky -c ~/.config/conky/neet_countdown.lua &
```

## Notes

- You can add this to your startup applications to load it on boot.
- Make sure you have compositing enabled if transparency doesn't work.
- Adjust `gap_x`, `gap_y`, and font sizes to suit your screen and taste.

## License

MIT or public domain. Use freely.
