# Speakeasy source provenance

The bundled `speakeasy/` directory contains the 25-page Markdown copy of [Speakeasy's API Design Guide](https://www.speakeasy.com/api-design) and all 24 locally referenced images. It was copied from the user's existing archive without changing the article or image bytes.

- Upstream repository: [speakeasy-api/developer-docs](https://github.com/speakeasy-api/developer-docs).
- Pinned source revision: `7330fc12ca86f540a39c621791703287ca0e190b`.
- Snapshot date: October 4, 2026.
- [Original manifest](speakeasy/manifest.json): source URLs, original source paths/checksums, Markdown paths, and asset mappings.
- [Upstream license](speakeasy/LICENSE): retained MIT license and copyright notice.
- [Bundle checksums](speakeasy/bundle-checksums.json): SHA-256 values for the files actually shipped here.

The archive's Markdown conversion preserves author wording and code, removes React imports/layout wrappers, converts callouts/tabs to Markdown, and rewrites guide links and images to local paths. It preserves upstream technical claims, typos, duplicated passages, and examples. The malformed Collections URL in the Request Body chapter is preserved; reach Collections through [topic-map.md](topic-map.md).

Only the readable guide, assets, original manifest, and license are shipped in this skill. Original manifest `source_file` entries refer to the archive's upstream Markdown/MDX tree, which is not bundled. Its source hashes identify those upstream files, not the converted Markdown. The original downloaded archive remains the maintenance source for untouched upstream files and conversion scripts.

`SKILL.md`, the topic map, interpretation notes, and review/refactor workflows are editorial additions. The source snapshot is a baseline, not a claim that the live website or protocols have been checked for every later change. Normal use should work from local references; look up current standards, tools, or requirements when the task needs current information.

When updating the snapshot, review upstream changes, preserve attribution and image paths, update the original manifest, regenerate bundle checksums, and reconcile the topic map and interpretation notes. Do not silently mix article revisions. Use the original manifest's URLs when a reader needs public source links; use local paths for the agent's reference reads.
