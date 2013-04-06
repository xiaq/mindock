# mindock

`mindock` is a minimal, programmable dock for herbstluftwm (and possibly other
tiling WMs).

## Why another dock?

[EWMH](http://standards.freedesktop.org/wm-spec/wm-spec-1.3.html) defines 2
properties of the root window to store the list of the windows:
`_NET_CLIENT_LIST` and `_NET_CLIENT_LIST_STACKING`. The former shall be in
"initial mapping order, starting with the oldest window". It's also the order
most stacking WMs use for "Alt-Tab" or like; therefore all docks and panels I
know of (awn, xfce4-panel, etc.) place windows in this order.

However, tiling WMs allow you to adjust the layout of windows, and the order
of navigation is likely changed too. In that case the navigation order becomes
inconsistent with `_NET_CLIENT_LIST`. Unfortunately, there seems to be no way
the WM can indicate the navigation order under this condition.

## Why dock at all? Why not just display a list of window names in dzen?

Docks are much more scalable and intuitive.

## How it works

It follows the model of [dzen](http://robm.github.io/dzen/): it monitors stdin
continuously, and when there is a new line of input, it parses it as a list of
X window IDs. Icons for these windows are then displayed, with the active
window in a different background.

Therefore this requires that you write a script for monitor the list of window
IDs on current workspace, which implies is that your WM has to be scriptable
so that you can monitor and output the list of windows in the first place. I
develop this dock under
[herbstluftwm](http://wwwcip.cs.fau.de/~re06huxa/herbstluftwm/)(hlwm) and for
hlwm; `hlwm-monitor-wid` is a reference bash script just for that.

To use with hlwm, just run

    ./hlwm-monitor-wid | ./mindock

## Roadmap

It's obvious that a lot is missing, but it's already usable for me. :)

Planned:

* `setup.py` things

* Prettier look (transparency, highlight effect, etc.)

Probably:

* Make icon clicking actually work :)

_Not_ planned:

* System tray

* Graphical configuration interface
