# Terminal Survival & Documentation Reference

## 1. Navigating Manual Pages (`man`)
When offline or auditing a binary on bare metal, `man` pages are the primary source of truth, but they are notoriously dense.
* **Open Manual:** `man [command]`
* **Search Forward:** Type `/` followed by your search term (e.g., `/recursive`).
* **Navigate Matches:** Press `n` to jump to the next match, and `N` to jump to the previous match.
* **Exit:** Press `q`.

## 2. Shell Built-ins vs. External Binaries (`help`)
* **For Bash Built-ins (`cd`, `echo`, `export`, `jobs`, `kill`):** 
  Do not waste time with `man`. Use `help [command]` for a clean, concise syntax breakdown. 
  * *Paging huge outputs:* `help [command] | less`
* **For External Binaries (`ps`, `df`, `du`, `setfacl`):** 
  Use `man [command]` or `--help`.

## 3. Minimalist / Container Constraints (e.g., Alpine Linux)
Bare-bones containers or minimal installations often strip out heavy documentation packages (like man pages) to keep images tiny.
* **Fallback Strategy:** Always try `[command] -h` or `[command] --help` first if `man` is missing.
