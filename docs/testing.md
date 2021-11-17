# Testing

## Default extension testing

this has a footnote[^1], and supports PVE, PMG, and PBS.

!!! note "title"
    This is an admonition

```yaml
edit_uri: https://github.com/proxmoxer/docs/edit/main/docs/

nav:
  - Home: index.md
  - Setup: setup.md
  - Testing: testing.md
  - Tools:
      - tools/index.md
      - Blocking Tasks: tools/blocking_tasks.md
```

| Command(s)        | Package   |
| ----------------- | --------- |
| bash              | bash      |
| ps, kill          | procps    |
| usermod, groupmod | passwd    |
| sed               | sed       |
| xargs             | findutils |

[^1]: footnote contents
*[PVE]: Proxmox Virtual Environment

## pymdownx extensions testing

!!! note "superfences"
    ```python
    def asdf():
      return
    ```


???+ warning "Details"
    ```python
    def asdf():
      return
    ```


=== "Python"
    ```python
    def main():
      print("Hello World")
    main()
    ```


=== "Javascript"
    ```javascript
    function main(){
      console.log("Hello World")
    }
    main()
    ```


--8<-- "all.md"
