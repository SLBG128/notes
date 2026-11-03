# Study Notes

**Author:** h1m_1208

This repository is the source for my study notes and writeups.
The notes are also published on my [personal website](https://h1m1208.github.io/notes/).

## Organization

- `articles/` — standalone technical articles.
- `pentesting/` — notes grouped by topic, such as Active Directory, exploits,
  and general techniques.
- `writeup/` — lab and room writeups.

The website preserves this directory structure in its navigation tree. Markdown
files in these folders are rendered as pages with the website's header, footer,
and shared styles. The repository's top-level `README.md` is documentation for
the source repository and is not published as a note.

## Writing notes

- Keep notes in the folders above; the website discovers Markdown files
  automatically during its Pages build.
- Use relative paths for images stored alongside a note. For example, from
  `writeup/tryhackme/recruit/recruit.md`, link to an image as
  `![Description](./img/img1.png)`.
- Preserve the folder structure when moving a note or its assets so relative
  links continue to work.
- Notes without Jekyll front matter are supported; the website build adds the
  layout metadata without changing the source files in this repository.

The website rebuilds this content when its Pages workflow runs. It checks for
updates daily, and can also be run manually from the website repository's
**Actions** tab.
