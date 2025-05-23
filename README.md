<div align="center"><h1><a href="https://www.galaxyweblinks.com/" target="_blank">Galaxy Weblinks</a></h1></div>

# WPML - Code Snippets

![Licence](https://img.shields.io/badge/Unlicense-red)

## Overview

A curated collection of code snippets and functions designed to optimize and improve **WordPress** and **WPML** websites. These resources can be used to enhance functionality, clean up code, and streamline development processes.

**Note:** Please be careful and make backups!

## WPML

- [ADD Language to body class](#add-language-to-body-class)
- [ADD page slug default language to body class](#add-page-slug-default-language-to-body-class)

---

## WPML

### ADD Language to body class

```php
/**
 * ADD Language to body class
 */
if ( !function_exists( 'gwl_body_class' ) ) {
	function gwl_body_class( $classes ) {
		
		// Add language slug to body classes
		if ( defined( 'ICL_LANGUAGE_CODE' ) )
			
			$classes[] = ICL_LANGUAGE_CODE;

		return $classes;
	}
}
add_filter( 'body_class', 'gwl_body_class' );
```

### ADD page slug default language to body class

```php
/**
 * ADD page slug default language to body class
 */
if ( ! function_exists( 'gwl_body_class' ) ) {

	function gwl_body_class( $classes ) {

		global $post;
		$default_lang = apply_filters( 'wpml_default_language', NULL );

		if ( ! ( $default_lang === ICL_LANGUAGE_CODE ) ) {
			if ( is_page() ) {

				$default_lang_id = apply_filters( 'wpml_object_id', $post->ID, 'page', TRUE, $default_lang );
				$classes[]  = sanitize_html_class( get_post_field( 'post_name', $default_lang_id ) );
			}
		}
		return $classes;
	}
}
add_filter( 'body_class', 'gwl_body_class' );
```

---

## License

This repository is unlicense[d], so feel free to fork.
