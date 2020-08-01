<div align="right">
  Язык:
  <a title="Английский" href="../../README.md">🇺🇸</a>
  <a title="Китайский" href="../zh-CN/README.md">🇨🇳</a>
  🇷🇺
</div>

![NexT preview](https://user-images.githubusercontent.com/16272760/83972923-98baae80-a915-11ea-8142-3cf875dad8bf.png)

<a title="NexT website" href="https://theme-next.js.org"><img align="right" alt="NexT logo" width="100" height="100" src="https://raw.githubusercontent.com/next-theme/hexo-theme-next/master/source/images/logo.svg?sanitize=true"></a>

# NexT

> «NexT» — элегантная высококачественная тема под [Hexo](https://hexo.io). Сделана с нуля, с любовью.

[![NPM version](https://img.shields.io/npm/v/hexo-theme-next?color=red&logo=npm&style=flat-square)](https://www.npmjs.com/package/hexo-theme-next)
[![Required Hexo version](https://img.shields.io/badge/hexo-%3E=4.0.0-blue?style=flat-square&logo=hexo)](https://hexo.io)
[![License](https://img.shields.io/badge/license-%20AGPL-orange?style=flat-square&logo=gnu)](https://github.com/next-theme/hexo-theme-next/blob/master/LICENSE.md)
[![Code Quality](https://img.shields.io/lgtm/grade/javascript/github/next-theme/hexo-theme-next?label=code%20quality&logo=lgtm&style=flat-square)](https://lgtm.com/projects/g/next-theme/hexo-theme-next/)
[![Build Status](https://img.shields.io/github/workflow/status/next-theme/hexo-theme-next/Linter?label=test&logo=github&style=flat-square)](https://github.com/next-theme/hexo-theme-next/actions?query=workflow%3ALinter)
[![Build Status](https://img.shields.io/github/workflow/status/next-theme/hexo-theme-next/Tester?logo=github&style=flat-square)](https://github.com/next-theme/hexo-theme-next/actions?query=workflow%3ATester)

## Демо

<p align="center">
  💟 <a href="https://theme-next.js.org/muse/">Muse</a> | 🔯 <a href="https://theme-next.js.org/mist/">Mist</a> | ♓️ <a href="https://theme-next.js.org/pisces/">Pisces</a> | ♊️ <a href="https://theme-next.js.org">Gemini</a>
<br>
<br>
  Больше примеров «NexT» <a href="https://github.com/next-theme/awesome-next#live-preview">здесь</a>.
</p>

## Установка

If you're using Hexo 5.0 or later, the simplest way to install is through npm:

```sh
$ cd hexo-site
$ npm install hexo-theme-next
```

Or you can clone the entire repository:

```sh
$ cd hexo-site
$ git clone https://github.com/next-theme/hexo-theme-next themes/next
```

See [detailed installation instructions][docs-installation-url] if you want any other variant.

## Configuration

At present, NexT encourages users to use the [Alternate Theme Config][docs-configuration-url] to configure NexT. And it's easy to customize the layout or style of NexT using [Custom Files][docs-custom-files-url].

It is not recommended to directly modify any files in the NexT theme. Because this may cause errors (e.g. merge conflicts), and the modified files may be discarded when upgrading the theme.

However, you can bypass merge conflicts (error message like **«Commit your changes or stash them before you can merge»**) by using the `Commit`, `Stash` or `Reset` commands for local changes. See [here](https://stackoverflow.com/a/15745424/5861495) how to do it.

## Плагины

Plugins extend and expand the functionality of NexT. There are two types of plugins: core plugins and third-party plugins. The core plugins are required by the basic functions of NexT. Third-party plugins are loaded from jsDelivr CDN by default, and they provide a large number of optional features.

Configuring these plugins is very easy. Например, Вы хотите использовать `pjax` для своего сайта. Открываем конфиг NexT'а и находим:

```yml
# Easily enable fast Ajax navigation on your website.
# For more information: https://github.com/next-theme/pjax
pjax: true
```

### Configure CDN

If you want to specify the CDN provider for any plugins, you need to set / update the CDN URL.

For example, if you want to set the CDN URL for `mediumzoom`, go to NexT config and see:

```yml
vendors:
  # ...
  # Some contents...
  # ...
  mediumzoom: # Set or update mediumzoom CDN URL.
```

## Обновление

NexT выпускает новые версии каждый месяц. You can update NexT by the following command.

Install the latest version throuth npm:

```sh
$ cd hexo-site
$ npm update hexo-theme-next
```

Or update to latest master branch:

```sh
$ cd themes/next
$ git pull
```

А если всплывают ошибки во время обновления (что-то наподобии **«Commit your changes or stash them before you can merge»**), рекомендуется ознакомиться с особенностью хранения [Alternate Theme Config][docs-configuration-url].\
Как бы то ни было, можно обойти ошибки при обновлении если «Закомитить», «Стэшнуть» или «Откатить» локальные изменения. Смотрим  [здесь](https://stackoverflow.com/a/15745424/5861495) как это сделать.

**Если нужно обновиться с версии v5.x / v7.x на последней версиями, читаем [здесь][docs-update-5-1-x-url].**

## Обратная связь

* Посетите [Awesome NexT][awesome-next-url] список.
* Вступить в наши [Gitter][gitter-url] чаты.
* [Добавить или улучшить перевод][i18n-url] за несколько секунд.
* Сообщить об ошибке в разделе [GitHub Issues][issues-bug-url].
* Запросить новую возможность на [GitHub][issues-feat-url].
* Голосовать за [популярные запросы возможностей][feat-req-vote-url].

## Contributing

We welcome you to join the development of NexT. Please see [contributing document][contributing-document-url]. 🤗

Also, we welcome Issue or PR to our [official-plugins][official-plugins-url].

## Содействие

[![Contributors][contributors-image]][contributors-url]

## Благодарности

«NexT» send special thanks to these great services that sponsor our core infrastructure:

<a href="https://github.com"><img height="40" src="https://github.githubassets.com/images/modules/logos_page/GitHub-Logo.png"></a>

> GitHub allows us to host the Git repository and run the test suite.

<a href="https://www.netlify.com"><img height="40" src="https://www.netlify.com/img/press/logos/full-logo-light.svg"></a>

> Netlify allows us to distribute the documentation.

<a href="https://crowdin.com"><img height="40" src="https://support.crowdin.com/assets/logos/crowdin-logo-small-black.svg"></a>

> Crowdin allows us to translate conveniently the documentation.

<a href="https://www.jsdelivr.com"><img height="40" src="https://raw.githubusercontent.com/jsdelivr/jsdelivr-media/master/default/svg/jsdelivr-logo-horizontal.svg"></a>

> Thanks jsDelivr for providing public CDN service.

[docs-installation-url]: https://theme-next.js.org/docs/getting-started/installation.html
[docs-configuration-url]: https://theme-next.js.org/docs/getting-started/configuration.html
[docs-custom-files-url]: https://theme-next.js.org/docs/theme-settings/custom-files.html
[docs-update-5-1-x-url]: https://theme-next.js.org/docs/getting-started/update-from-v5.html

[gitter-url]: https://gitter.im/hexo-next
[i18n-url]: https://crowdin.com/project/hexo-theme-next

[awesome-next-url]: https://github.com/next-theme/awesome-next
[issues-bug-url]: https://github.com/next-theme/hexo-theme-next/issues/new?assignees=&labels=Bug&template=bug-report.md
[issues-feat-url]: https://github.com/next-theme/hexo-theme-next/issues/new?assignees=&labels=Feature+Request&template=feature-request.md
[feat-req-vote-url]: https://github.com/next-theme/hexo-theme-next/issues?q=is%3Aopen+is%3Aissue+label%3A%22Feature+Request%22

[contributing-document-url]: https://github.com/next-theme/hexo-theme-next/blob/master/.github/CONTRIBUTING.md
[official-plugins-url]: https://github.com/next-theme
[contributors-image]: https://raw.githubusercontent.com/next-theme/contributors/master/contributors.svg
[contributors-url]: https://github.com/next-theme/hexo-theme-next/blob/master/docs/AUTHORS.md