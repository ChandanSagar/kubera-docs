---
title: Informationen zu GitHub Pages
intro: 'Mit {% data variables.product.prodname_pages %} können Sie eine Website zu Ihrer Person, Ihrer Organisation oder Ihrem Projekt direkt aus einem {% data variables.product.product_name %}-Repository hosten.'
redirect_from:
  - /articles/what-are-github-pages/
  - /articles/what-is-github-pages/
  - /articles/user-organization-and-project-pages/
  - /articles/using-a-static-site-generator-other-than-jekyll/
  - /articles/mime-types-on-github-pages/
  - /articles/should-i-rename-usernamegithubcom-repositories-to-usernamegithubio/
  - /articles/about-github-pages
product: '{% data reusables.gated-features.pages %}'
versions:
  free-pro-team: '*'
  enterprise-server: '*'
---

### Informationen zu {% data variables.product.prodname_pages %}

{% data variables.product.prodname_pages %} ist ein Hosting-Dienst für statische Websites, der HTML-, CSS- und JavaScript-Dateien direkt aus einem Repository auf {% data variables.product.product_name %} bezieht, diese Dateien optional einem Build-Prozess unterzieht und eine Website veröffentlicht. Beispiele für {% data variables.product.prodname_pages %}-Websites findest Du in der [{% data variables.product.prodname_pages %}-Beispielsammlung](https://github.com/collections/github-pages-examples).

{% if currentVersion == "free-pro-team@latest" %}
You can host your site on
{% data variables.product.prodname_dotcom %}'s `github.io` domain or your own custom domain. Weitere Informationen finden Sie unter „[Eine benutzerdefinierte Domain mit {% data variables.product.prodname_pages %} verwenden](/articles/using-a-custom-domain-with-github-pages)“.
{% endif %}

Informationen zu den ersten Schritten findest Du unter „[Eine {% data variables.product.prodname_pages %}-Website erstellen](/articles/creating-a-github-pages-site).“

{% if currentVersion == "free-pro-team@latest" or currentVersion ver_gt "enterprise-server@2.22" %}
Organization owners can disable the publication of
{% data variables.product.prodname_pages %} sites from the organization's repositories. For more information, see "[Disabling publication of {% data variables.product.prodname_pages %} sites for your organization](/github/setting-up-and-managing-organizations-and-teams/disabling-publication-of-github-pages-sites-for-your-organization)."
{% endif %}

### Arten von {% data variables.product.prodname_pages %}-Websites

Es gibt drei Arten von {% data variables.product.prodname_pages %}-Websites: Projekt-, Benutzer- und Organisations-Websites. Projekt-Websites sind mit einem bestimmten Projekt verbunden, das auf {% data variables.product.product_name %} gehostet wird, z. B. einer JavaScript-Bibliothek oder einer Rezeptsammlung. Benutzer- und Organisations-Websites sind mit einem bestimmten {% data variables.product.product_name %}-Konto verbunden.

To publish a user site, you must create a repository owned by your user account that's named {% if currentVersion == "free-pro-team@latest" %}`<user>.github.io`{% else %}`<user>.<hostname>`{% endif %}. To publish an organization site, you must create a repository owned by an organization that's named {% if currentVersion == "free-pro-team@latest" %}`<organization>.github.io`{% else %}`<organization>.<hostname>`{% endif %}. {% if currentVersion == "free-pro-team@latest" %}Unless you're using a custom domain, user and organization sites are available at `http(s)://<username>.github.io` or `http(s)://<organization>.github.io`.{% endif %}

Die Quelldateien für eine Projekt-Website werden im selben Repository gespeichert wie das zugehörige Projekt. {% if currentVersion == "free-pro-team@latest" %}Unless you're using a custom domain, project sites are available at `http(s)://<user>.github.io/<repository>` or `http(s)://<organization>.github.io/<repository>`.{% endif %}

{% if currentVersion == "free-pro-team@latest" %}
Weitere Informationen dazu, wie sich die URL Ihrer Website bei benutzerdefinierten Domains ändert, finden Sie unter „[Informationen zu benutzerdefinierten Domains und {% data variables.product.prodname_pages %}](/articles/about-custom-domains-and-github-pages)“.
{% endif %}

Sie können für jedes {% data variables.product.product_name %}-Konto nur eine Benutzer- oder Organisations-Website erstellen. Für Projekt-Websites gibt es keine Beschränkung, egal, ob sie einer Organisation oder einem Benutzerkonto gehören.

{% if enterpriseServerVersions contains currentVersion %}
The URL where your site is available depends on whether subdomain isolation is enabled for
{% data variables.product.product_location %}.

| Art der Website | Subdomänen-Isolation aktiviert | Subdomänen-Isolation deaktiviert |
| --------------- | ------------------------------ | -------------------------------- |
|                 |                                |                                  |
 Benutzer | 

`http(s)://pages.<hostname>/<username>/<repository>/` | `http(s)://<hostname>/pages/<username>/<repository>/` | Organisation | `http(s)://pages.<hostname>/<organization>/<repository>/` | `http(s)://<hostname>/pages/<organization>/<repository>/` | Projekt-Website, die einem Benutzerkonto gehört | `http(s)://pages.<hostname>/<username>/<repository>/` | `http(s)://<hostname>/pages/<username>/<repository>/` Projekt-Website, die einer Organisation gehört | `http(s)://pages.<hostname>/<orgname>/<repository>/` | `http(s)://<hostname>/pages/<orgname>/<repository>/`

Weitere Informationen findest Du unter „[Subdomänen-Isolation aktivieren](/enterprise/{{ currentVersion }}/admin/installation/enabling-subdomain-isolation)“. Bei Fragen kannst Du Dich auch an den Websiteadministrator wenden.
{% endif %}

{% if currentVersion == "free-pro-team@latest" %}
{% note %}

**Hinweis:** Repositorys, die das alte Namensschema `<user>.github.com` verwenden, werden noch veröffentlicht, aber Besucher werden von `http(s)://<username>.github.com` auf `http(s)://<username>.github.io` weitergeleitet. Wenn sowohl ein `<user>.github.com`- als auch ein `<user>.github.io`-Repository vorhanden sind, wird nur das `<user>.github.io`-Repository veröffentlicht.

{% endnote %}
{% endif %}

### Veröffentlichungsquellen für {% data variables.product.prodname_pages %}-Websites

The publishing source for your {% data variables.product.prodname_pages %} site is the branch and folder where the source files for your site are stored.

{% data reusables.pages.private_pages_are_public_warning %}

{% if currentVersion == "free-pro-team@latest" or currentVersion ver_gt "enterprise-server@2.22" %}

If the default publishing source exists in your repository, {% data variables.product.prodname_pages %} will automatically publish a site from that source. The default publishing source for user and organization sites is the root of the default branch for the repository. The default publishing source for project sites is the root of the `gh-pages` branch.

If you want to keep the source files for your site in a different location, you can change the publishing source for your site. You can publish your site from any branch in the repository, either from the root of the repository on that branch, `/`, or from the `/docs` folder on that branch. Weitere Informationen findest Du unter „[Eine Veröffentlichungsquelle für Deine {% data variables.product.prodname_pages %}-Website konfigurieren](/articles/configuring-a-publishing-source-for-your-github-pages-site#choosing-a-publishing-source).“

If you choose the `/docs` folder of any branch as your publishing source, {% data variables.product.prodname_pages %} will read everything to publish your site{% if currentVersion == "free-pro-team@latest" %}, including the _CNAME_ file,{% endif %} from the `/docs` folder.{% if currentVersion == "free-pro-team@latest" %} For example, when you edit your custom domain through the {% data variables.product.prodname_pages %} settings, the custom domain will write to `/docs/CNAME`. Weitere Informationen zu _CNAME_-Dateien findest Du unter „[Eine benutzerdefinierte Domäne für Deine {% data variables.product.prodname_pages %}-Website verwalten](/articles/managing-a-custom-domain-for-your-github-pages-site)“.{% endif %}

{% else %}

Die standardmäßige Veröffentlichungsquelle für Benutzer- und Organisations-Websites ist der `master`-Branch. Wenn das Repository Deiner Benutzer- oder Organisations-Website einen `master`-Branch aufweist, wird Deine Website automatisch von diesem Branch veröffentlicht. Du kannst keine andere Veröffentlichungsquelle für Benutzer- oder Organisations-Websites auswählen.

Die standardmäßige Veröffentlichungsquelle für Projekt-Websites ist der `gh-pages`-Branch. Wenn das Repository Deiner Projekt-Website einen `gh-pages`-Branch aufweist, wird Deine Website automatisch von diesem Branch veröffentlicht.

Du kannst Projekt-Websites auch vom `master`-Branch oder einem `/docs`-Ordner auf dem `master`-Branch veröffentlichen. Um Deine Website aus einer dieser Quellen zu veröffentlichen, musst Du eine andere Veröffentlichungsquelle konfigurieren. Weitere Informationen findest Du unter „[Eine Veröffentlichungsquelle für Deine {% data variables.product.prodname_pages %}-Website konfigurieren](/articles/configuring-a-publishing-source-for-your-github-pages-site#choosing-a-publishing-source).“

 If you choose the `/docs` folder of the `master` branch as your publishing source, {% data variables.product.prodname_pages %} will read everything to publish your site{% if currentVersion == "free-pro-team@latest" %}, including the _CNAME_ file,{% endif %} from the `/docs` folder.{% if currentVersion == "free-pro-team@latest" %} For example, when you edit your custom domain through the {% data variables.product.prodname_pages %} settings, the custom domain will write to `/docs/CNAME`. Weitere Informationen zu _CNAME_-Dateien findest Du unter „[Eine benutzerdefinierte Domäne für Deine {% data variables.product.prodname_pages %}-Website verwalten](/articles/managing-a-custom-domain-for-your-github-pages-site)“.{% endif %}

 Du kannst Deine Projekt-Website nicht aus einem anderen Branch veröffentlichen, auch wenn der Standard-Branch nicht `Master` oder `gh-pages` ist.

{% endif %}

### Generatoren für statische Websites

{% data variables.product.prodname_pages %} veröffentlicht alle statische Dateien, die Sie zu Ihrem Repository pushen. Sie können eigene statische Dateien erstellen oder einen Generator für statische Websites verwenden, der die Website für Sie erstellt. Darüber hinaus können Sie Ihren eigenen Build-Prozess lokal oder auf einem anderen Server anpassen. Wir empfehlen Jekyll, einen Generator für statische Websites mit integrierter Unterstützung von {% data variables.product.prodname_pages %} und einem vereinfachten Build-Prozess. Weitere Informationen finden Sie unter „[Informationen zu {% data variables.product.prodname_pages %} und Jekyll](/articles/about-github-pages-and-jekyll)“.

{% data variables.product.prodname_pages %} verwendet standardmäßig Jekyll für die Erstellung Ihrer Website. Wenn Sie einen anderen Generator für statische Websites als Jekyll verwenden möchten, müssen Sie den Jekyll-Build-Prozess deaktivieren. Erstellen Sie dazu im Root Ihrer Veröffentlichungsquelle eine leere Datei mit dem Namen `.nojekyll` und folgen den Anweisungen des gewünschten Generators, um Ihre Website lokal zu erstellen.

{% data variables.product.prodname_pages %} unterstützt keine serverseitigen Sprachen wie PHP, Ruby oder Python.

### Richtlinien für die Verwendung von {% data variables.product.prodname_pages %}

{% if currentVersion == "free-pro-team@latest" %}
- {% data variables.product.prodname_pages %}-Websites, die nach dem 15. Juni 2016 und mittels `github.io`-Domains erstellt wurden, werden über HTTPS bereitgestellt. Wenn Du Deine Website vor dem 15. Juni 2016 erstellt hast, kannst Du die HTTPS-Unterstützung für den Traffic zu Deiner Website aktivieren. Weitere Informationen findest Du unter „[{% data variables.product.prodname_pages %}-Website mit HTTPS schützen](/articles/securing-your-github-pages-site-with-https).“
- {% data reusables.pages.no_sensitive_data_pages %}
- Ihre Nutzung von {% data variables.product.prodname_pages %} unterliegt den [GitHub-Nutzungsbedingungen](/articles/github-terms-of-service/), einschließlich des Weiterverkaufsverbots.

#### Nutzungseinschränkungen
{% endif %}
{% data variables.product.prodname_pages %} unterliegen den folgenden Nutzungseinschränkungen:

  - {% data variables.product.prodname_pages %} source repositories have a recommended limit of 1GB.{% if currentVersion == "free-pro-team@latest" %} For more information, see "[What is my disk quota?"](/articles/what-is-my-disk-quota/#file-and-repository-size-limitations){% endif %}
  - Veröffentlichte {% data variables.product.prodname_pages %}-Websites dürfen nicht größer als 1 GB sein.
{% if currentVersion == "free-pro-team@latest" %}
  - {% data variables.product.prodname_pages %} sites have a *soft* bandwidth limit of 100GB per month.
  - {% data variables.product.prodname_pages %} sites have a *soft* limit of 10 builds per hour.

Wenn Ihre Website diese Nutzungskontingente überschreitet, kann Ihre Website ggf. nicht bedient werden oder Sie erhalten eine höfliche E-Mail von {% data variables.contact.contact_support %}, in der Strategien vorgeschlagen werden, um die Auswirkung Ihrer Website auf unsere Server zu reduzieren. Dazu zählen das Einsetzen eines Drittanbieter-CDNs (Content Distribution Networks) vor Ihrer Website, die Nutzung anderer {% data variables.product.prodname_dotcom %}-Features, beispielsweise Veröffentlichungen, oder der Wechsel zu einem anderen Hosting-Dienst, der ggf. besser zu Ihren Anforderungen passt.

#### Verbotene Verwendungen

{% data variables.product.prodname_pages %} soll oder darf nicht als kostenloser Web-Hosting-Dienst zum Betreiben Ihrer Online-Geschäfts-, E-Commerce-Website oder jeder anderen Website verwendet werden, die in erster Linie darauf ausgerichtet ist, kommerzielle Transaktionen zu erleichtern oder kommerzielle Software-as-a-Service-Lösungen (SaaS) bereitzustellen.

Zusätzlich darf in {% data variables.product.prodname_pages %}-Websites Folgendes nicht enthalten sein:

  - Illegale oder gemäß unseren [Nutzungsbedingungen](/articles/github-terms-of-service/) oder den [Community-Richtlinien](/articles/github-community-guidelines/) untersagte Inhalte oder Aktivitäten
  - Gewalttätige oder bedrohende Inhalte oder Aktivitäten
  - Übermäßig automatisierte Massenaktivitäten (beispielsweise Spam)
  - GitHub-Benutzer oder GitHub-Dienste kompromittierende Aktivitäten
  - Schnell-reich-werden-Schemas
  - Sexuell anstößige Inhalte
  - Deine Identität oder den Zweck Deiner Website falsch darstellende Inhalte
If you have questions about whether your use or intended use falls into these categories, please contact

{% data variables.contact.contact_support %}.
{% endif %}

### MIME-Typen auf {% data variables.product.prodname_pages %}

Ein MIME-Typ ist ein Header, den ein Server an einen Browser übermittelt und der Informationen zur Art und zum Format der Dateien enthält, die der Browser angefordert hat. {% data variables.product.prodname_pages %} unterstützt mehr als 750 MIME-Typen bei Tausenden von Dateierweiterungen. Die Liste der unterstützten MIME-Typen wird aus dem [mime-db-Projekt](https://github.com/jshttp/mime-db) erzeugt.

Zwar können Sie keine benutzerdefinierten MIME-Typen für einzelne Dateien oder Repositorys festlegen. Sie können jedoch MIME-Typen für die Verwendung auf {% data variables.product.prodname_pages %} hinzufügen oder ändern. Weitere Informationen findest Du in den [Beitragsrichtlinien für mime-db](https://github.com/jshttp/mime-db#adding-custom-media-types).

### Weiterführende Informationen

- [{% data variables.product.prodname_pages %}](https://lab.github.com/githubtraining/github-pages) auf {% data variables.product.prodname_learning %}
- "[{% data variables.product.prodname_pages %}](/v3/repos/pages)"