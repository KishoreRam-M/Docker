
**Linked Clone (VM)** — a child VM that **references a parent VM disk** and stores only its own changes.

## Short & sweet subtopics

* **Definition:** Shortcut VM that borrows the parent disk and keeps a small “diff” file.
* **How it works:** Child VM points to parent disk for unchanged files; writes only new/modified files to its delta.
* **Storage example:** Parent 10 GB + child diffs (e.g., 200 MB) vs full clones (10 GB each).
* **Benefits:** Saves disk space, fast to create, great for testing.
* **Limitations:** Depends on parent (delete parent → clones break), not easily portable, possible small perf hit.
* **Analogy:** Master textbook in library + student sticky notes.
* **Key fact:** Child runs as its own VM but **refers** to parent disk (parent must exist, not necessarily run).

**One-liner:** Linked Clone = your own VM that keeps only the changes and borrows the rest from the parent.
