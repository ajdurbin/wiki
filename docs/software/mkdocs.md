# Installation #
Using pip, `pip install mkdocs`

Create a project with `mkdocs new my-project` and `cd my-project`

Start the server with `mkdocs serve -dev-addr=0.0.0.0:80 &` or whatever port you want

Build the site with mkdocs build to create the `site` directory

Edit `mkdocs.yml` to change the theme to readthedocs, title, author, name pages differently, etc.

Add new `.md` files in separate directories as necessary for desired layout

Add MathJaX extensions with `extra_javascript:
- <"https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-MML-AM_CHTML"> in `mkdocs.yml`

# links #
- <https://github.com/Python-Markdown/markdown/wiki/Third-Party-Extensions#math--latex>
- <https://www.mkdocs.org/user-guide/configuration/#formatting-options>
- <https://stackoverflow.com/questions/27882261/mkdocs-and-mathjax>

# hyperlinks
Require `<>` tags to be marked up.

# convert dokuwiki markup
```
# convert markup
import os

if __name__ == '__main__':
    wiki_files = []
    for root, directories, filenames in os.walk('./wiki_files/'):
        for filename in filenames:
            if filename.endswith('.txt'):
                wiki_files.append(os.path.join(root, filename))
    for wiki_file in wiki_files:
        with open(wiki_file, 'r') as infile:
            lines = infile.readlines()
        new_lines = []
        for line in lines:
            new_line = line.replace(r"===", r"#").\
                replace(r"''", r"`").\
                replace(r"<code>", r"```").\
                replace(r"</code>", r"```").\
                replace(r"  -", r"-").\
                replace(r"  *", r"*")
            new_lines.append(new_line)
        new_filename = wiki_file.\
            replace(r"wiki_files", r"wiki/docs").\
            replace(r".txt", r".md")
        new_directory = '/'.join(new_filename.split('/')[:-1])
        try:
            os.mkdir(new_directory)
        except:
            pass
        with open(new_filename, 'w') as outfile:
            for line in new_lines:
                outfile.write(line)
```
And for converting the majority of hyperlinks:
```
import os

if __name__ == '__main__':
    wiki_files = []
    for root, directories, filenames in os.walk('./wiki/docs/'):
        for filename in filenames:
            if filename.endswith('.md'):
                wiki_files.append(os.path.join(root, filename))
    for wiki_file in wiki_files:
        with open(wiki_file, 'r') as infile:
            text = infile.readlines()
        new_lines = []
        for line in text:
            words = line.split()
            new_words = []
            for word in words:
                if 'http' in word:
                    new_words.append('<' + word.replace(r"`", r"") + '>')
                else:
                    new_words.append(word)
            new_lines.append(' '.join(new_words))
        with open(wiki_file, 'w') as outfile:
            for line in new_lines:
                outfile.write(line + '\n')
```
