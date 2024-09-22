# Koodariverstas proto
- This is my workt trainee proto website 
## version 100

- Here are the necessary files for MediaWiki 1.42.1 to customize MediaWiki. The site contains Bootstrap elements, but the site takes breakpoints and page styles from the tweekitemplate.php file.
- The three breakpoints on the site ensure that no box gets hidden behind another when the screen size changes.

- The table of contents is generated from custom divs defined in the localsettings, which fetch a list of links based on the pages stored under that category.
- Additionally, in MediaWiki, users are always guided to select the correct category when creating a new page. When choosing a category,
- the page template also includes a couple of dropdown menus to facilitate site navigation.

- MediaWiki also includes a custom footer, which is defined in the LocalSettings.php file. This was done to ensure that the footer images are properly arranged when the display size scales.

- Then the actions menu is defined in the MediaWiki:tweeki.js file. When a user edits or deletes a page, this code captures the parameters of the page being modified.

  Here is the mediawiki:tweeki.js code:
  $(document).ready(function() {

    var pageName = mw.config.get('wgPageName');
    var editLink = mw.util.getUrl(pageName) + '?action=edit';
    var loginLink = mw.util.getUrl('Special:UserLogin');

    $('#footer-edit-link').attr('href', editLink);
    $('#footer-login-link').attr('href', loginLink);
});
$(document).ready(function() {
    if ($('#custom-dropdown-menu').length === 0) {
        // Luo kontaineri dropdown-valikolle
        $('.navbar-nav').append('<div id="custom-dropdown-menu"></div>');

       
        var pageName = mw.config.get('wgPageName');

      
        var editLink = mw.util.getUrl(pageName) + '?action=edit';
        var editSourceLink = mw.util.getUrl(pageName) + '?action=edit&mode=source';
        var loginLink = mw.util.getUrl('Special:UserLogin');
        var protectLink = mw.util.getUrl(pageName) + '?action=protect';
        var deleteLink = mw.util.getUrl(pageName) + '?action=delete';

        
        var dropdownMenu = `
            <li class="nav-item dropdown">
                <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                    Actions
                </a>
                <div class="dropdown-menu" aria-labelledby="navbarDropdown">
                    <a class="dropdown-item" href="${editLink}">Edit</a>
                    <a class="dropdown-item" href="${editSourceLink}">Edit Source</a>
                    <a class="dropdown-item" href="${protectLink}">Protect</a>
                    <a class="dropdown-item" href="${deleteLink}">Delete</a>
                    <a class="dropdown-item" href="${loginLink}">Login</a>
                </div>
            </li>
        `;

      
        $('#custom-dropdown-menu').append(dropdownMenu);
        
        if (!mw.config.get('wgUserName')) {
            $('#navbarDropdown').find('.dropdown-item:lt(4)').hide();
        }
    }
    $('.dropdown-toggle').dropdown();
});

And here is classes what are defined on mediawiki:tweeki.css file:
.nav-item.dropdown .dropdown-menu {
    display: none;
}

.nav-item.dropdown.show .dropdown-menu {
    display: block;
}
@media (max-width: 600px) {
    main {
        width: 100%;
    }
}
