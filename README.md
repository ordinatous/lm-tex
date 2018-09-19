# Lettre de motivation avec Tex

## Le Tex

Lorsque vous "éditez" du texte , soit vous faites votre mise en page au fur et à mesure
soit vous faites tout à la fin.

Et le résultat n'est pas toujours à la hauteur.

Je ne suis pas non plus un expert en Tex , cependant avec un peu de recherche , on trouve les infos
nécessaire pour adapter les documents les plus simples.

On trouve des modèles pour :
* des livres
* des projets
* des CV
* des Lettres de motivations
* des présentations

Ces documents sont très élégants, vous en trouverez à cette adresse:
* http://www.LaTeXTemplates.com

## La Lettre de Motivations

Le modèle que je propose est une modification de celui disponible ici:
* http://www.kindoblue.nl/articles/cover-letter-part1

En m'inspirant de ce post:
* https://tex.stackexchange.com/questions/196360/scrlttr2-make-second-page-footer-match-first-page-footer

Car ma lettre était trop longue et je souhaitais que le recruteur conserve mes coordonnées si il perdait la première page.

### Décomposition du document
#### Les commentaires

En première partie du fichier vous trouverez les commentaires avec les sources ainsi que la licence.

Vous remarquerez donc que l'on commente une ligne avec `%`.
```Tex
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% Lettre de motivation
% LaTeX Template
% Version 1.2 (24/01/2018)
% Auteur originale :
% http://www.kindoblue.nl/articles/cover-letter-part1
%
% Modifié afin d'obtenir un pied de page sur la seconde page
% identique au premier pied de page.
% Je me suis inspiré de ce post:
% Source: https://tex.stackexchange.com/questions/196360/scrlttr2-make-second-page-footer-match-first-page-footer
% License:
% CC BY-NC-SA 3.0 (http://creativecommons.org/licenses/by-nc-sa/3.0/)
%
% IMPORTANT: A COMPILER AVEC LuaTEX OU XeLaTeX
%
% J'utilise la font Roboto-Light , très standard et légère à l'oeil.
%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

```
### Configurations

J'ai francisé en partie le document.

Vous remarquerez la première ligne `\documentclass{scrlttr2}` , qui défini la classe de document .
Il en existent d'autres tel que:

|class | utilisation |
|------|------------|
|article | 	For articles in scientific journals, presentations, short reports, program documentation, invitations, ...|
|IEEEtran| 	For articles with the IEEE Transactions format.|
|proc    | 	A class for proceedings based on the article class.|
|report  | 	For longer reports containing several chapters, small books, thesis, ...|
|book    | 	For real books.|
|slides  | 	For slides. The class uses big sans serif letters.-
|memoir  | 	For changing sensibly the output of the document. It is based on the book class, but you can create any kind of document with it [1]|
|letter  | 	For writing letters.|
|beamer  | 	For writing presentations (see LaTeX/Presentations).|

Ces *class* peuvent être accompagnée d'options , ici la taille de la *font* est défini à 12;
par défaut elle est à 10 :

```
\documentclass[12pt]{article}
\usepackage{blindtext}
\begin{document}
\blindtext
\end{document}
```
Mais là n'est pas le sujet...
L'édition en `TeX` demande quelques packages pour obtenir l'effet attendu , par exemple on peut créer des réferences et les liens vers les sites à visiter.

Cette fonction réclame ces packages particulier:

```tex
\usepackage{hyperref}
\usepackage{xspace}
```
On créera ensuite son lien avec cette commande:

* Exemple:
* `% \def\reference{\href{https://lien.web}{reference}\xspace}`

* Vrai lien
* `\def\ordinatous{\href{https://ordinatous.com}{}\xspace}`

Le lien sera alors cliquable.

```
%----------------------------------------------------------------------------------------
%	PACKAGES ET AUTRES CONFIGURATIONS DU DOCUMENT
%----------------------------------------------------------------------------------------

\documentclass{scrlttr2}
\usepackage{blindtext}

\usepackage{fontspec} % Autorise la customization
\usepackage{marvosym} % Autorise l'utilisation des symbols
\usepackage[french]{babel} % Requis pour compiler avec Windows
\usepackage{hyperref}
\usepackage{xspace}
\setlength\parindent{0pt} % Enlève les indentations des paragraphes

\defaultfontfeatures{Mapping=tex-text}
\setmainfont {Roboto-Light.ttf} % Font du document
\setsansfont {Roboto-Light.ttf} % Used in the from address line above the to address


\renewcommand{\normalsize}{\fontsize{12}{17}\selectfont} % Sets the font size and leading


```

### Informations Personnelles

Vous devinez que c'est ici que l'on indique ses informations personnelles, on crée et défini les variables
qui seront appelées dans le document.

Il ne faut modifier que le texte entre les accolades `{}` .

```
%----------------------------------------------------------------------------------------
%  INFORMATIONS PERSONNELLES
%----------------------------------------------------------------------------------------

\setkomavar{fromname}{George Abitbol} % Votre nom
\setkomavar{fromaddress}{255 Route de Pétaouchnock\\Pétaoucnock} % Votre adresse
\setkomavar{fromphone}{(+33) 102030405} % Votre N° de Tel
\setkomavar{fromemail}{george.abitbol@gmail.com} % Votre adresse courriel
\setkomavar{place}{Pétaoucnock} % Indiquez la ville qui apparaitra devant la date
\setkomavar{signature}{George Abitbol} % Votre nom pour la signature
\setkomavar{fromurl}{https://george.abitbol.com/CV/} % Your personal website
% These are not used in this document, uncomment if you would like to use them and refer to them as \usekomavar{name}

```

### En tête et pied de page

C'est ici que j'ai bricolé le modèle original . On constate que les variables => `\setkomavar` `{fromname}`, `{fromaddress}`, `{fromemail}`, `{fromphone}`, `{fromurl}` sont appelées.

Des petits logos ont même étaient ajouté:
`Letter`, `Telefon`, `at`.

Et finalement 1 nouvelle variable est crée: `{nextfoot}` et `{firstfoot}` est utilisée ici.

```
%----------------------------------------------------------------------------------------
%  HEADER SECTION
%----------------------------------------------------------------------------------------

\setkomavar{firsthead}{
	\centering
	{\addfontfeature{LetterSpace=15.0}\fontsize{36}{36}\selectfont\scshape \usekomavar{fromname}}\\[5mm]
	\fontsize{21}{21}\selectfont\scshape {L'Homme le classe du Monde } % Le poste pour lequel vous candidatez

\setkomavar{firstfoot}{\parbox{\textwidth}{\centering%
		{%
			\renewcommand{\\}{~{\large\textperiodcentered}~}%
			\usekomavar{fromaddress}%
		}\\%
		{\normalsize\Letter} \usekomavar{fromemail} \ {\Large\Telefon} \usekomavar{fromphone} \\
		{\normalesize\at} \usekomavar{fromurl}% Ajouter
	}
}%
%Simplement réutiliser les variables
\setkomavar{nextfoot}{\usekomavar{firstfoot}}
%----------------------------------------------------------------------------------------

```

### Le contenu de la lettre

On démarre l'édition par `\begin{document}` .
On indique les retours à la ligne avec `\\` .
Il est possible de de faire une liste avec :

```
\begin{document}

%----------------------------------------------------------------------------------------
% Contenu de la lettre
%----------------------------------------------------------------------------------------

\begin{letter}{ % Addresse de la société ou vous postulez
Monsieur le Président de
la Société la plus classe du Monde\\
Direction des ressources humaines\\

}

\setkomavar{subject}{Acte de Candidature} % On indique l'objet de notre lettre ici

\opening {Madame, Monsieur;}

Avant de se pencher sur le latin, vous pouvez visiter mon site : \ordinatous.com .

Lorem ipsum is a pseudo-Latin text used in web design, typography, layout, and printing in place of English to emphasise design elements over content. \\

BlaBlaBla \\

\begin{itemize}
	\item Direction Interministérielle du Numérique et du Système d'Information et de Communication de l'État
	\item Socle Interministériel de Logiciel Libre
	\item Référentiel Général d'Interopérabilité
	\item ou encore la Circulaire Ayrault du 19 septembre 2012
\end{itemize}


Cicero's version of Liber Primus (first Book), sections 1.10.32–3:\\

Blablabla \\


Souhaitant avoir retenu votre attention et dans l'attente d'une réponse de votre part , je reste disponible pour un complément d'informations et un éventuel entretien .

Veuillez trouver ici l'expression de mes sincères salutations.

\closing{}
%----------------------------------------------------------------------------------------
\end{letter}
\end{document}
```

### La liste en Tex

Voici comment créer une liste :

```
\begin{itemize}
	\item Bla
	\item Ble
	\item Bli
	\item Blo
\end{itemize}

```

### Editeur de texte

La particularité du Tex et LaTex est que vous *editez* votre fichier avec un éditeur de texte , un vrai comme
* [NotePad++](https://notepad-plus-plus.org/)
* [Atom](https://atom.io/)
* [Kate](https://kate-editor.org/get-it/)
* [Gedit](https://wiki.gnome.org/Apps/Gedit)

Bon ok , ce n'est pas ce qu'il y a de plus sexy pour commencer, par contre vous pourrez oublier NotePad et WordPad .

Le must c'est [TexStudio](https://www.texstudio.org/) qui vous permettra de lancer le *processeur* de document .

Pour les *windowsien* voici un lien pour compiler l'application qui a besoin de *perl* [TexUserGroup](https://www.tug.org/texlive/windows.html)

## Sources

[Minimalia](http://www.kindoblue.nl/articles/cover-letter-part1"Modèle original")

[LaTex-Project](https://www.latex-project.org/about/"Site du projet LaTex")

[Donald Knuth](https://www-cs-faculty.stanford.edu/~knuth/"Site de l'inventeur du Tex")

[TexBlog](https://texblog.org/2013/02/13/latex-documentclass-options-illustrated/)

[Wikibooks](https://en.wikibooks.org/wiki/LaTeX/Document_Structure#Document_classes)

[ShareLatex](https://www.sharelatex.com/learn/Creating_a_document_in_LaTeX)

[StackExchange](https://tex.stackexchange.com)

[TUG](https://www.tug.org/"TexUserGroup")
