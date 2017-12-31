# Hugo Theme
A Hugo theme intended for use with R [blogdown](https://github.com/rstudio/blogdown). Forked from [tuftesque](https://github.com/nstrayer/tuftesque) and [Hugo-Tufte](https://github.com/shawnohare/hugo-tufte).

## Get Started
For use with RStudio and blogdown follow the excellent [instructions](https://bookdown.org/yihui/blogdown/) from Yihui Xie, Amber Thomas, and Alison Hill.

Install the blogdown package in R.
```r
## Install from CRAN
install.packages("blogdown")
## Or, install from GitHub
if (!requireNamespace("devtools")) install.packages("devtools")
devtools::install_github("rstudio/blogdown")
```

Install Hugo using blogdown (works in Windows, macOS, and Linux)
```r
blogdown::install_hugo()
```

Finally, create the site and get the blogdown-tufte theme.
```r
blogdown::new_site()
blogdown::install_theme('nstrayer/tuftesque')
```
The blogdown instructions provide everything else you need to know for serving up a website using Rmarkdown or markdown right in RStudio.

## Rmarkdown Features

### Margin notes

To use the side notes in Rmarkdown, install the `tufte` package.
```r
## Install from CRAN
install.packages("tufte")
```

Side notes are generated this way in Rmarkdown (not markdown documents) using the following inline chunk:
```r
tufte::margin_note("Your margin note text")
```
This will allow you to include any Rchunk output into the margin note. See Shortcodes section below on how to accomplish this using plain markdown.

## Page Parameters

- `excerpt` string: Include summary or exceprt from the post to display under the post title on main page.
- `hideDate` boolean: if true, do not display a page date.  When `meta` is set to
  true, `hideDate` takes greater precedence.
- `hideReadTime` boolean: if true, do not display the page's reading time
  estimate.  When `meta` is set to true, `hideReadTime` takes greater precedence.
- `math` boolean: if true, try to render the page's LaTeX code using MatheJax. 
- `meta` boolean: if true, display page metadata such as author, date, categories provided
  these page parameters exist and are not overridden.  Content in the `/post` directory,
  (i.e., pages of type "post") ignore this parameter.
- `toc` boolean: if true, display the table of contents for the page.

## Shortcodes

- `blockquote`
  - **Description**: Wrap text in a blockquote and insert optional
  `cite` or `footer` metadata.
  - **Usage**: Accepts the named parameters `cite` and `footer`.
  - **Example**: 
  ```html
  {{% blockquote cite="www.shawnohare.com" footer="Shawn" %}}
    There is nothing more beautiful than an elegant mathematical proof. 
  {{% /blockquote %}}`
  ```

- `div`
   - **Description**: This shortcode is provided as a work-around for wrapping
   complex blocks of markdown in div tags. The wrapped text can
   include other shortcodes
   - **Usage**: Identical to the `section` shortcode.
   Accepts the style parameters `class` and `id`.
   If only the positional argument `"end"` is passed, a closing tag
   will be inserted.
   - **Example**: `{{< div class="my-class" >}}` inserts a 
   `<div class="my-class">` tag, while
   `{{<div "end" >}}` inserts the closing `</div>` tag.

- `epigraph`
  - **Description**: Create an epigraph with the wrapped text.
  - **Usage**: To include a footer with source attribution, pass in the
  optional named parameters `pre`, `cite`, `post`. These parameters 
  make no styling assumptions, so spacing is important.  A more compactly
  styled epigraph will be used if the `type` parameter is set to `compact`.
  - **Example**:
  ```
  {{% epigraph pre="Author Writer, " cite="Math is Fun" %}}
  This is an example of an epigraph with some math 
  \\( \mathbb N \subseteq \mathbb R \\)
  to start the beginning of a section.
  {{% /epigraph %}}
  ```

- `marginnote`
  - **Description**: Wrap text to produce a numberless margin note.
  - Usage: Accepts a required positional argument that is the margin note id.
  `{{% marginnote "<margin note id>"" %}}...{{% /marginnote %}}`
  - **Example**: `{{% marginnote "mn-example" %}}Some marginnote{{% /marginnote%}}`

- `section`
   - **Description**: This shortcode is provided as a work-around for wrapping
   complex blocks of markdown in section tags. The wrapped text can
   include other shortcodes
   - **Usage**: Accepts the style parameters `class` and `id`.
   If only the positional argument `"end"` is passed, a closing tag
   will be inserted.
   - **Example**: `{{< section class="my-class" >}}` inserts a 
   `<section class="my-class">` tag, while
   `{{<section "end" >}}` inserts the closing `</section>` tag.


- `sidenote`
  - **Description**: Wrap text to produce an automatically numbered sidenote.
  - **Usage**: identical to `marginnote`. 
  Accepts a required positional argument that is the side note id.
  `{{% sidenote "<side note id>"" %}}...{{% /sidenote %}}`
  - **Example**: `{{% sidenote "sn-example" %}}Some sidenote{{% /sidenote %}}`

## Site Parameters

Add or change the following site parameters in `config.toml`

### General site options
Within `[params]`
- `showPoweredBy` boolean: if true, display a shoutout to Hugo and this theme.
- `copyrightHolder` string: Inserts the value in the default copyright notice.
- `copyright` string: Custom copyright notice.
- `backgroundcolor` string: Inserts value for page background, defaults to `#fffff8`

### Main menu
Add direct links for the main menu by adding additional `[[menu.main]]` entries (note that links are relative):
```
[[menu.main]]
    name = "About"
    url = "/About/"
[[menu.main]]
    name = "CV"
    url = "/CV/"
```

### Social media links
Add social media links in the footer by adding `[[params.social]]` entries using [Fontawesome icons](http://fontawesome.io/icons/).
```
    [[params.social]]
    name = "GitHub"
    icon = "github"
    link = "https://github.com/rstudio/blogdown"
    [[params.social]]
    name = "Twitter"
    icon = "twitter"
    link = "https://twitter.com/rstudio"
    [[params.social]]
    name = "LinkedIn"
    icon = "linkedin-square"
    link = "https://www.linkedin.com/"
    [[params.social]]
    name = "Instagram"
    icon = "instagram"
link = "https://www.instagram.com/"
```

:construction: Work in progress :construction: