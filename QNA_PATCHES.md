# qna patches

This fork of longbridge/gpui-fast carries the GPUI patches of
[gpui-mcp](https://github.com/themixednuts/gpui-mcp) (`vendor/gpui`, cut from
Zed `16c9aa7ea6`), ported onto GPUI Fast's retained rendering:

- frame observation (`frame_observer.rs`, `Window::observe_frames`,
  `Window::focus_observed_element`), the `frame_node`/`frame_text` element hooks
  and the `frame_metadata`/`frame_action`/`frame_redacted` builders;
- `aria_disabled`/`aria_hidden`/`aria_read_only`;
- programmatic focus and text input, and pointer ownership (`PointerState`);
- font-family fallback that keeps weight, style and features;
- CSS grid track lists, and the view-cache observation (`ViewDraw`).

Where GPUI Fast replays a retained stretch of a frame (`fast/retained.rs`,
`fast/splice.rs`), the observed nodes of that stretch are replayed with it
(`FrameCheckpoint`). Known gap: a replayed view is not redrawn when the
redaction boundary around it changes (gpui-mcp's `ObservationChanged`).
