<table align="center" style="border-collapse:collapse !important; border:none !important;">
  <tr style="border:0px none; border-top: 0px none !important;">
    <td align="center" valign="middle" style="padding:0 1rem; border:none !important;">
      <a href="https://www.w3.org/TR/2011/WD-html5-20110405/" target="_blank">
        <img src="https://vardumper.github.io/extended-htmldocument/html5_logo-with-wordmark.svg" style="display:block; height:90px; width:auto; max-width:300px;" alt="HTML5 Logo" />
      </a>
    </td>
    <td align="center" valign="middle" style="padding:0 1rem; border:none !important;">
      <a href="https://symfony.com" target="_blank">
        <img src="https://vardumper.github.io/extended-htmldocument/symfony_black_03.svg" style="display:block; height:100px; width:auto; max-width:220px;" alt="Symfony Logo" />
      </a>
    </td>
    <td align="center" valign="middle" style="padding:0 1rem; border:none !important;">
      <a href="https://ux.symfony.com/twig-component" target="_blank">
        <img src="https://vardumper.github.io/extended-htmldocument/twig-component.png" style="display:block; height:100px; width:auto; max-width:220px;" alt="Twig Component Logo" />
      </a>
    </td>
  </tr>
</table>
<h1 align="center">Twig Components for HTML5 Elements</h1>

<p dir="auto" align="center"><a href="https://packagist.org/packages/vardumper/html5-twig-component-bundle" rel="nofollow"><img src="https://camo.githubusercontent.com/6a9ae6cc08f06f37eb7ded1283ca4ea01b8a932983b40db638f4e77c246a2277/68747470733a2f2f706f7365722e707567782e6f72672f76617264756d7065722f68746d6c352d747769672d636f6d706f6e656e742d62756e646c652f762f737461626c65" alt="Latest Stable Version" data-canonical-src="https://poser.pugx.org/vardumper/html5-twig-component-bundle/v/stable" style="max-width: 100%;"></a>
<a href="https://packagist.org/packages/vardumper/html5-twig-component-bundle" rel="nofollow"><img src="https://camo.githubusercontent.com/b6c67f12e11c01f06759b7f274e57270f4c415cb3293f85158e628213d4f9edb/68747470733a2f2f706f7365722e707567782e6f72672f76617264756d7065722f68746d6c352d747769672d636f6d706f6e656e742d62756e646c652f646f776e6c6f616473" alt="Total Downloads" data-canonical-src="https://poser.pugx.org/vardumper/html5-twig-component-bundle/downloads" style="max-width: 100%;"></a>
<a href="https://dtrack.erikpoehler.us/projects/404a3506-2b62-4a9e-8617-e80f3ebb1f03" rel="nofollow"><img src="https://camo.githubusercontent.com/5f252a080d33632162f81a86ad07811b851bbf20facd24b6d581f85bcd4e94e9/68747470733a2f2f64747261636b2e6572696b706f65686c65722e75732f6170692f76312f62616467652f76756c6e732f70726f6a6563742f34303461333530362d326236322d346139652d383631372d6538306633656262316630333f6170694b65793d6f64745f4a354f4b7a394a6357704b416e717a383077687854767741336f516a47424779" alt="Vulnerabilities for html5-twig-component-bundle" data-canonical-src="https://dtrack.erikpoehler.us/api/v1/badge/vulns/project/404a3506-2b62-4a9e-8617-e80f3ebb1f03?apiKey=odt_J5OKz9JcWpKAnqz80whxTvwA3oQjGBGy" style="max-width: 100%;"></a></p>

This is a Symfony Bundle which adds pre-built, typesafe, auto-generated Twig Components for all HTML5 elements. It comes with full WCAG, ARIA support, also adds support for Alpine.js attributes. It makes use of [Extended HTMLDocument](https://github.com/vardumper/extended-htmldocument) which is a schema-first library that improves HTML5 support in PHP 8.4. Mainly used for validation of immutable enum attributes.

This is especially useful when writing anonymous Twig Components enforcing standards-compliance, always-valid HTML5.

## Features

- **Symfony UX Integration**: Native Symfony Twig Component support
- **ARIA Compliant**: Complete ARIA attribute support with proper validation
- **Auto-Generated**: Consistent API across all HTML5 elements via schema-first approach
- **Enum Validation**: Static attribute validation for HTML compliance
- **Modern PHP**: Requires PHP 8.4+ for DOM\HTMLDocument features

## Requirements
* PHP 8.4 – the underlying Extended HTMLDocument library is built upon PHPs DOM\HTMLDocument which is available since PHP 8.4+

Since only the Enums are used for attribute validation here, adding support for older PHP versions could be done easily if it's needed or requested.

## Installation

```bash
composer require vardumper/html5-twig-component-bundle
```

The bundle includes automatic service registration - no additional configuration needed!

## Configuration

The bundle is automatically registered via Symfony Flex. If you need to register it manually, add to `config/bundles.php`:

```php
# config/bundles.php
return [
    // ...
    Html\TwigComponentBundle\HtmlTwigComponentBundle::class => ['all' => true],
];
```

Next, tell Symfony that Twig Components can be found in a new path. Edit `config/packages/twig_component.yaml` and add the following:

```yaml
# config/packages/twig_component.yaml
twig_component:
    defaults:
        Html\TwigComponentBundle\Twig\: '%kernel.project_dir%/vendor/vardumper/html5-twig-component-bundle/src/Twig/'
```

All Twig Components are automatically discovered and registered through the bundle's DependencyInjection extension. No manual service configuration required!

## Usage

Use any HTML element as a Twig Component:

```twig
<twig:Blockquote cite="https://example.com">
    This is a quote from example.com
</twig:Blockquote>

<twig:Button role="button" type="submit">
    Submit Form
</twig:Button>

<twig:Input type="email" name="email" required />
```

### Use in anonymous Twig Components
```twig
{# templates/components/Teaser.html.twig #}
<twig:Div class="teaser"> 
    <twig:H3>{{ headline }}</twig:H3>
    <twig:P>{{ content }}</twig:P>
    <twig:A role="button" href="{{ buttonLink }}" title="{{ buttonText }}">{{ buttonText }}</twig:A>
</twig:Div>
```

which can then be used in pages:
```twig
{# templates/page.html.twig #}
{% for item in teasers %}
    <twig:Teaser 
        headline="{{ item.headline }}" 
        content="{{ item.content }}" 
        buttonLink="{{ item.buttonLink }}" 
        buttonText="{{ item.buttonText }}">
    </twig:Teaser>
{% endfor %}
```

### Passing arrays as component props
You can pass associative arrays to component props using the `:` notation. For example to pass `data-*` attributes to the component:
```twig
<twig:Div :dataAttributes="{'role': 'article'}">
    Hello world
</twig:Div>
```

This will render a `data-role="article"` attribute on the generated component's root element.
## Features

- ✅ All HTML5 elements supported
- ✅ Full ARIA attributes support
- ✅ Type-safe enum validation
- ✅ PreMount validation with OptionsResolver
- ✅ Proper namespace structure (Block/Inline/Void)

## Components Structure

Components are organized by type:
- `Block` - Block-level elements (div, section, article, etc.)
- `Inline` - Inline elements (span, a, strong, etc.)
- `Void` - non-rendered elements (head, wbr, meta, etc.)


## Read More
* [Extended HTMLDocument Documentation](https://vardumper.github.io/extended-htmldocument/)
* [Extended HTMLDocument Github Repository](https://github.com/vardumper/extended-htmldocument)
* [Twig Components](https://symfony.com/bundles/ux-twig-component/current/index.html)
* [Symfony UX](https://ux.symfony.com/)

## Issues & Bugs

Please report issues in this packages home at [Extended HTMLDocument](https://github.com/vardumper/extended-htmldocument)
