``markdown
# Melponum

## Table of Contents

1. [Project Overview](#project-overview)
2. [Text Transcription Protocol](#text-transcription-protocol)
3. [Encoding Protocol](#encoding-protocol)



<a name="project-overview"></a>

## Project Overview

Melponum (Melpomène à l’heure numérique - Melpomene in the Digital Age) is a project aimed at fostering wider engagement with French Renaissance drama. Although the number of editions and critical studies has grown considerably over the last hundred years, these texts remain absent from French secondary school curricula (where theatre-related curricula are restricted to 17th-21st centuries) and from contemporary stages. The project therefore brings together researchers, teachers from secondary and higher education, and performing arts professionals to make the full diversity of Renaissance theatre more accessible (from classical genres and so-called ‘medieval forms’ to neo-Latin drama).

To make these plays more accessible and restore them to their rightful place within French heritage, we are producing digital editions in three editorial formats: a “research” edition, featuring a non-modernised text with full scholarly annotations; a “teaching” edition, presenting a modernised text with ready-to-use classroom sequences; a ‘rehearsal’ edition, offering a dedicated layout and dramaturgical notes. Despite their distinct purposes, the three types of edition share common features: explanatory notes on language and cultural references, as well as links to recordings of readings or performances produced or collected through the project.

To support and promote these digital editions, we are developing a scientific and cultural outreach programme, which includes conferences featuring performances, public talks coupled with staged readings, theatre workshops at universities co-led by an actor and a researcher, workshops and talks in secondary schools, and the organisation of school trips around these Renaissance plays.



<a name="text-transcription-protocol"></a>

## Text Transcription Protocol

### Original Text

We have chosen a semi-diplomatic transcription, meaning that we carry out an initial normalization without preserving all the information present in the manuscript. The following normalization principles are applied:

* resolution of abbreviations;
* conversion of the ampersand *\&* to *et*, long *s* (*ſ*) to *s*, and *ß* to *ss*;
* disambiguation of *i/j* and *u/v*;
* addition of diacritical accents (on *a/à*; *la/là*; *ou/où*; on past participles of first-group verbs; and on potential homonyms);
* separation of agglutinated forms according to modern usage (*lautre* becomes *l’autre*).

The original punctuation and decorative initials (lettrines) are retained. Capital letters are preserved, including their diacritical accents where present.

Typographical errors are corrected directly, but the correction is indicated by square brackets and the erroneous reading is reported in a note. Reconstructed text is indicated by angle brackets (*plaint<es>*).

### Modernized Text

Modernization primarily affects spelling; words and constructions that remain obscure are explained in notes.

Spelling is not altered when doing so would affect syllable count or rhyme. In such cases, the editor explains in a note why the original spelling has been retained.

Some editors have also chosen, in the modernized version only, to intervene in punctuation and capitalization.

### Annotation

In keeping with the project’s aims, the editions are designed to address different types of audiences. Accordingly, annotations fall into three categories:

1. Notes for researchers: sources; references to other contemporary texts; interpretation; references to scholarship.
2. Notes for teachers and students: lexical and linguistic notes; clarification of mythological and historical allusions; pronunciation notes (*e* muet, dieresis, synaeresis).
3. Notes for directors and actors: entrances and exits of characters; props; acting directions (movement, tone, expression). This also includes the list of characters at the beginning of an act when it is absent from the original text.



<a name="encoding-protocol"></a>

## Encoding Protocol

### Organization of the Text Body

The `<text>` element contains the textual content of the work and is divided into three parts: `<front>`, `<body>`, and `<back>`.

The `<front>` element contains the scholarly editor’s introduction, the title page `<titlepage>`, preliminary texts, as well as the cast list `<castlist>` and the title of the play. The `<body>` contains the play itself along with its prologues and epilogues, while `<back>` gathers the closing materials.

The `<div>` element is used to indicate textual divisions. Its `@type` attribute is essential for distinguishing sections: it takes values such as `preface`, `argument`, `title`, `other`, `dedication`, `poem`, `letter` in the `<front>` and `<back>` sections, and values such as `act`, `scene`, `play`, `journee`, `sequence`, `prologue`, `epilogue` in the `<body>`. Numbering of these divisions is managed via the `@n` attribute, notably for acts, scenes, journées, and sequences.

The titles of these divisions are encoded using the `<head>` element, whether they are titles of acts, scenes, journées, or preliminary texts. Prose paragraphs are marked up with `<p>`. Text excerpts cited by the scholarly editor in the introduction are marked up with the `<q>` element.



### Cast List

The cast list is a crucial element of the `<front>` and is encoded using the `<castList>` element. This tag includes a `<head>` for the list title and at least one `<castItem>` indicating a role. If the list is missing or incomplete in the source text, it is reconstructed by the scholarly editor and inserted into the critical apparatus (`<app>` with a `<note type="dramaturgy">`), in which case its title becomes “Les personnages”. Each `<castItem>` must contain a `<role>` element, which carries the unique identifier of the character via the `@xml:id` attribute, or an `<actor>` element when necessary. The `@xml:id` attribute is built from the first three significant letters of the play’s title, followed by an underscore and the character’s name without accents, in lowercase. The `@gender` attribute is mandatory and takes the values `male`, `female`, or `undefined`. The character’s name is also encoded using `<name>`, specifying whether it refers to a group or a single person via the `@type` attribute. A description of the role may be provided in `<roleDesc>`. Related roles may be grouped within a `<castGroup>`.



### Dialogue, Stage Directions, and Verse

Each character’s speech is contained within an `<sp>` element, which requires the `@who` attribute to identify the speaker using the character’s unique identifier. The speaker’s name as it appears in the source text is encoded with the `<speaker>` element. When a character’s name is accompanied by a specification (for example, “the peasant”), this is marked up with `<roleName>` inside `<speaker>`.

Stage directions and other scenic indications are marked up with `<stage>`. This element uses the `@type` attribute to specify the nature of the indication (`setting`, `entrance`, `exit`, `noise`, etc.). Additional attributes such as `@who` and `@toWhom` may be used to designate the characters concerned by the stage direction, using the play’s specific character identifiers. When stage directions are added by the scholarly editor, the element is embedded within a critical apparatus (`<app>` containing a `<note type="dramaturgy">`).

In verse plays, each verse is encoded using the `<l>` element and, when verses form stanzas, these are grouped within `<lg>`. When a verse is split across several speeches in the source edition, the `@part` attribute is used with the values `I`, `M`, or `F`.

Specific typographical conventions of the source text, such as a maxim marked by quotation marks, may be noted using the attribute `@rend="marginalQuotes"`.

Column changes within a dialogue or a group of verses are indicated by the self-closing `<cb/>` element.



### Representation of Variants, Corrections, and Modernizations

The management of variations and corrections between the source text and its transcription or modernization is handled by the `<choice>` element. This tag contains pairs of elements encoding two versions of the same passage. The `<orig>` and `<reg>` pair is used to distinguish original spelling from modernized spelling, while the `<sic>` and `<corr>` pair signals an error in the source text and its correction by the editor. Since abbreviations are resolved directly during transcription, the `<abbr>` and `<expan>` pair is not used.



### Notes and Critical Apparatus

The critical apparatus is materialized by the `<app>` element, which must always contain at least one `<note>` tag. Notes by the scholarly editor must be included within this apparatus. The `<note>` element requires the `@type` attribute, which must take one of the predefined values: `dramaturgy`, `meaning`, or `philology`. The `@resp` attribute is also mandatory in order to identify the editor responsible for the note.



### Other

Line breaks (`<lb/>`) are not encoded, except within `<titlePage>`. Page breaks are systematically encoded using the `<pb>` element, with the `@n` attribute indicating pagination or foliation.

Illustrations are encoded using `<figure>` (or `<notatedMusic>` for musical scores), which must contain the `<graphic>` tag for image placement (via the `@url` attribute) and `<desc>` for an image description.

Cross-references and links are managed using `<ref>`. When used with the `@target` attribute, it allows links to external resources or internal links to other parts of the text, typically when cited in notes or in the editors’ introduction. To mark the anchor point of a cited verse, the `<anchor>` element is placed at the beginning of the verse and carries a specific `@xml:id`.

The `<unclear>` element, with the attributes `@reason` and `@cert`, indicates text that is present but difficult to read. The `<gap/>` element, with the `@reason` attribute, indicates an omission of text due to damage or a deliberate choice by the author. `<supplied>` is used for text reconstructed by the editor or transcriber, as opposed to `<add>`, which encodes text inserted by an author or scribe. `<del>` is used for text struck through by the author. `<mentioned>` is used for words employed in mention.

Finally, certain typographical features are encoded using specific elements: `<c rend="lettrine">` for decorative initials, and `<hi rend="superscript">` for superscript characters. Titles of works are marked up with `<title>`. The `<foreign>` element is used for any word or expression in a language other than that of the surrounding context, with the language specified by the `@xml:lang` attribute in accordance with RFC 5646.

### Contributors

* Nina Hugot, project lead
* Milène Mallevays, research engineer
* Jérémy Sagnier, postdoctoral researcher
```
