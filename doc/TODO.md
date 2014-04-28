Tasks Needing Attention
=======================

The tasks are divided to short-term items - these need attention
in order to wrap up the current performance improvement phase
and are fairly detailed - and long-term items that outline more
general projects of whose development this project would benefit.

Most of these tasks require Java (or Scala, Groovy?) programming
and (willing to pick up) some UIMA knowledge.  However, if you
want to help out but aren't a programmer, there are tasks marked
as **NP** that are suitable for non-coders too!

Apologies if this list is not kept 100% up-to-date all the time.

Short-Term TODO
---------------

Quality:
  * NE-based clues and type coercion, for starters involving
    the OpenNLP NamedEntity extractor providing generic LATs
  * Generate LATs from meaningful SVs (consider "Who invented
    the transistor?" with LAT "person" (Who?) and SV "invent";
    derivation relations of "invent" include "inventor" which is
    a hyponym of "person", so generate an LAT!)
  * Use (WordNet) ontology relationships (synsets etc.) to generate
    extra clues; consider generating Clues also for CandidateAnswer
    and matching them similar to TyCor (ClueCor? :-)
  * Take Wordnet synsets into account in LATs
  * Better passage scoring?
  * Walk through the QA chapter of Taming Text to verify we are on
    quality parity. :)
  * Compare quality with blanqa to ensure quality parity?

Search:
  * Switch to SolrJ
  * SpanQuery?

Long-Term TODO
--------------

Parsing:
  * Take a very good look at the RegEx Link Grammar
    <http://wiki.opencog.org/w/RelEx>

Quality:
  * Check TyCor on TamingText dataset
  * Add more structured information sources!
    * DBPedia, FrameNet, Lemon, PATTY, PPDB
  * Extend WordNet ontology (so far used for TyCor) with more
    resources - dkpro lsr or uby
  * More advanced NE extraction, multi-word NEs, label-less LATs
    via NE clustering
  * Walk through IBM Watson papers and add more TODO items. :)
  * Evidence gathering feedback loops - initially maybe just
    a single feedback loop for candidate answer evidence gathering,
    but we may also gather evidence for LATs (and their synsets!) etc.

Performance Measurement:
  * Export full coefficient vectors of candidate answer and answer
    ranking, use that for parameter learning

Speed:
  * Multi-threaded CAS Processing - a massive boost!  Does this
    strictly require using UIMA-AS or can we do without it?
  * Persistent instances of expensive-to-initialize annotators
  * Shallower alternative to StanfordParser when parsing results?
    * For starters, POS tagging?
    * Try MSTParser with conll_mcd_order2_0.1.model, KenLM?

Interface:
  * Readline interface for the interactive IO?
  * Web interface.
  * Give context to answers, allow for clarifications and iterative
    conversation.

Janitorial:
  * Add an origin record to each annotation - which annotator
    produced it? Will be useful when we have multiple possible
    annotation paths.
  * Add a per-CAS singleton containing unique id, id of the
    spawning document and id of the originating CAS; this will
    enable tracing full origin of each CAS.
  * Switch from JWNL to JWI which seems to be much nicer to work with?
  * The type system distinction by pipeline phases does not work well;
    .tycor is a step in the right direction, but now CandidateAnswerCAS
    also has Focus from QuestionTypes, which does not fit in .tycor...

Datasets:
  * **NP** Clean up the TREC datasets - weed out questions that
    cannot be answered from Wikipedia, update out-of-date answers,
    remove too ambiguous questions(?)
  * **NP** Prepare a corpus of documents and associated questions
    that can be answered based on information from the documents.
  * **NP** Prepare a corpus of complex questions that require some
    inference.