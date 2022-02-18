# evote-movie-2022-07-current-page-link-styling

part of the evote-2022 project sequence

- [https://github.com/dr-matt-smith/evote-movie-2022](https://github.com/dr-matt-smith/evote-movie-2022)


## NOTES for this project step

Adding current page link styling in the navbar

- add to the beginning of `/templates/_header.php` a set of variables, one for each nav link. Each variable should be set to an empty string if the variable is not defined (when this template fragment is required-in by a page template). But if the variable already has a value, then that value should be used. Below we use the `??` **null coalescing** operator to do this. 


  ```php
      <?php
      $pageTitle = $pageTitle ?? '';
      
      $homePageStyle = $homePageStyle ?? '';
      $aboutPageStyle = $aboutPageStyle ?? '';
      $listPageStyle = $listPageStyle ?? '';
      $contactPageStyle = $contactPageStyle ?? '';
      $sitemapPageStyle = $sitemapPageStyle ?? '';
      ?>
      
      <!doctype html>
      ...
  ```

  - NOTE: if you are not happy using the `??` **null coalescing** operator you could just write an IF-statement something like this for each link style variable `if(empty($homePageStyle)){$homePageStyle = '';}`


- In the nav-bar links themselves of template `/templates/_header.php`, a CSS `class` is added to each link, whose value will be either an empty string or the value (`current_page`) from the style variable for each link. So, for example, the home page link will now be `<a href="/" class="<?= $homePageStyle ?>">Home</a>`, and so will be styled if variable `$homePageStyle` contains `current_page`:

    ```php
        ...
        <nav>
            <ul>
                <li>
                    <a href="/" class="<?= $homePageStyle ?>">Home</a>
                </li>

                <li>
                    <a href="/?action=about" class="<?= $aboutPageStyle ?>">About Us</a>
                </li>

                <li>
                    <a href="/?action=list" class="<?= $listPageStyle ?>">Movie ratings</a>
                </li>

                <li>
                    <a href="/?action=contact" class="<?= $contactPageStyle ?>">Contact Us</a>
                </li>

                <li>
                    <a href="/?action=sitemap" class="<?= $sitemapPageStyle ?>">Site Map</a>
                </li>
            </ul>
        </nav>
    ```

- add to the beginning of each page template a statement to set the nav style link variable for that page to be the string `current_page`. For example, here is the about page template, which sets variable `$aboutPageStyle` to `current_page` before requiring-in the `_header.php` template:

  ```php
      <?php
      $pageTitle = 'about page';
      $aboutPageStyle = 'current_page';
      require_once __DIR__ . '/_header.php';
      //---------------- footer ---------------
      ?>

      <h1>
          About us
      </h1>

      <p>
          We are EvoteMovie MGW
      </p>
      <p>
          We are based in Dublin.
      </p>
      <p>
          We were established in 2007.
      </p>
      <p>
          We sell computers and computer services - and host this great movie voting site!.
      </p>

      <?php
      //---------------- footer ---------------
      require_once __DIR__ . '/_footer.php';
      ?>
  ```
