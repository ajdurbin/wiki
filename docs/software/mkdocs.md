### Installation 
Using pip, `pip install mkdocs`

Create a project with `mkdocs new my-project` and `cd my-project`

Start the server with `mkdocs serve -dev-addr=0.0.0.0:80 &` or whatever port you want

Build the site with mkdocs build to create the `site` directory

Edit `mkdocs.yml` to change the theme to readthedocs, title, author, name pages differently, etc.

Add new `.md` files in separate directories as necessary for desired layout

Add MathJaX extensions with `extra_javascript:
  - "https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-MML-AM_CHTML"` in `mkdocs.yml`