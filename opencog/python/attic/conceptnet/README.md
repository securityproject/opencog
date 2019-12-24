## ConceptNet Converter for OpenCog

* This package is useful for mapping ConceptNet assertions into OpenCog atoms.
* For example, the ConceptNet relation 'IsA' ( denoted on the csv file as /r/IsA/)
is mapped to 'InheritanceLink', because their meanings are the same.
* Similarly, other relations can be mapped to OpenCog links by adding them to the
map_dict variable in the convert.py module.
* For ConceptNet relations that don't have an equivalent OpenCog link,
an EvaluationLink is used.
* In some cases a relation maybe mapped to more than
one link.

### Mapping
The following is a list of ConceptNet relation to OpenCog link mappings:
```
1. ConceptuallyRelatedTo -> IntensionalSimilarityLink
2. ThematicKLine -> IntensionalSimilarityLink
3. SuperThematicKLine -> IntensionalInheritanceLink
4. IsA -> InheritanceLink
5. PropertyOf -> InheritanceLink
6. DefinedAs -> SimilarityLink
7. PrerequisiteEventOf -> EvaluationLink PrerequisiteEventOf
8. FirstSubeventOf -> EvaluationLink FirstSubeventOf
9. SubeventOf -> EvaluationLink SubeventOf
10. LastSubeventOf -> EvaluationLink LastSubeventOf
11. EffectOf -> EvaluationLink EffectOf
             -> EvaluationLink
12. PartOf -> EvaluationLink PartOf
13. MadeOf -> EvaluationLink MadeOf
14. CapableOf -> EvaluationLink CapableOf
15. LocationOf -> EvaluationLink LocationOf
16. DesirousEffectOf -> EvaluationLink DesirousEffectOf
17. UsedFor -> EvaluationLink UsedFor
18. CapableOfReceivingAction -> EvaluationLink CapableOfReceivingAction
19. MotivationOf -> EvaluationLink MotivationOf
20. DesireOf -> EvaluationLink DesireOf
21. HasPrerequisite -> EvaluationLink HasPrerequisite
22. Causes -> EvaluationLink Causes
23. HasProperty -> IntensionalInheritanceLink
24. Desires -> EvaluationLink Desires
25. HasSubevent -> EvaluationLink HasSubevent
26. AtLocation -> EvaluationLink AtLocation
```

### Using
Procedure to create a scheme data file from the original conceptnet csv files:

1. Download the current csv tar ball from http://conceptnet5.media.mit.edu/downloads/current/
2. Extract the tarball contents into this folder
3. Run convert.py from the terminal

### Notes:
1. Instead of downloading and extracting the original files as in the above instructions, you
can also use the prepared test files, which can be found at:
https://github.com/opencog/test-datasets/tree/master/conceptnet
which includes the preprocessed output in conceptnet4.scm
2. Corpus = The word frequency csv file used to calculate the term probabilities. (60000_Word_Freqs.csv)
3. The output file in the same folder
4. You can load a result file in your Python code like
```python
from opencog.atomspace import AtomSpace, types

# If result file name is result.py
import result

# Your AtomSpace instance
a = AtomSpace()

# Load to your AtomSpace
result.load_concept_net(a, types)
```

### Example Inputs(conceptnet URI) and corresponding outputs:
1.
```scheme
/a/[/r/IsA/,/c/en/america_beautiful/,/c/en/national_anthem/]
	-->
(InheritanceLink (stv 1.0 0.5)
	(ConceptNode "america_beautiful" (stv 2.5245749935e-09 0.949999988079))
	(ConceptNode "national_anthem" (stv 2.5245749935e-09 0.949999988079))
)
```

2.
```scheme
/a/[/r/PartOf/,/c/en/ankara/,/c/en/central_anatolia_region/]
	-->
(EvaluationLink (stv 1.0 0.5)
	(PredicateNode "PartOf" (stv 2.5245749935e-09 0.949999988079))
	(ListLink
		(ConceptNode "ankara" (stv 2.5245749935e-09 0.949999988079))
		(ConceptNode "central_anatolia_region" (stv 2.5245749935e-09 0.949999988079))
	)
)
```

3.
```scheme
/a/[/r/AtLocation/,/c/en/apple_inc/,/c/en/apple_campus/]
	-->
(EvaluationLink (stv 1.0 0.5)
	(PredicateNode "AtLocation" (stv 2.5245749935e-09 0.949999988079))
	(ListLink
		(ConceptNode "apple_inc" (stv 2.5245749935e-09 0.949999988079))
		(ConceptNode "apple_campus" (stv 2.5245749935e-09 0.949999988079))
	)
)
```

4.
```scheme
/a/[/r/HasSubevent/,/c/en/type/,/c/en/think/]
	-->
(DuringLink (stv 1.0 0.5)
	(ConceptNode "type" (stv 8.42703138915e-06 0.949999988079))
	(ConceptNode "think" (stv 7.3313658504e-06 0.949999988079))
)
```

5.
```scheme
/a/[/r/DefinedAs/,/c/en/wool/,/c/en/hair_of_sheep/]
	-->
(SimilarityLink (stv 1.0 0.5)
	(ConceptNode "wool" (stv 1.15625534818e-05 0.949999988079))
	(ConceptNode "hair_of_sheep" (stv 2.5245749935e-09 0.949999988079))
)
```

6.
```scheme
/a/[/r/UsedFor/,/c/en/library/,/c/en/lend_book/]
	-->
(EvaluationLink (stv 1.0 0.5)
	(PredicateNode "UsedFor" (stv 2.5245749935e-09 0.949999988079))
	(ListLink
		(ConceptNode "library" (stv 6.12613366684e-05 0.949999988079))
		(ConceptNode "lend_book" (stv 2.5245749935e-09 0.949999988079))
	)
)
```

7.
```scheme
/a/[/r/Desires/,/c/en/person/,/c/en/intellectual_stimulation/]
	-->
(EvaluationLink (stv 1.0 0.5)
	(PredicateNode "Desires" (stv 2.5245749935e-09 0.949999988079))
	(ListLink
		(ConceptNode "person" (stv 0.000312100572046 0.949999988079))
		(ConceptNode "intellectual_stimulation" (stv 2.5245749935e-09 0.949999988079))
	)
)
```

8.
```scheme
/a/[/r/HasProperty/,/c/en/and_chew_tobacco/,/c/en/disgust/]
	-->
(IntensionalInheritanceLink (stv 1.0 0.5)
	(ConceptNode "and_chew_tobacco" (stv 2.5245749935e-09 0.949999988079))
	(ConceptNode "disgust" (stv 1.01487910342e-06 0.949999988079))
)
```

9.
```scheme
/a/[/r/HasPrerequisite/,/c/en/read_book/,/c/en/get_one/]
	-->
(RetroactiveImplicationLink (stv 1.0 0.5)
	(ConceptNode "read_book" (stv 2.5245749935e-09 0.949999988079))
	(ConceptNode "get_one" (stv 2.5245749935e-09 0.949999988079))
)
```

10.
```scheme
/a/[/r/CapableOf/,/c/en/couple/,/c/en/see_counselor/]
	-->
(EvaluationLink (stv 1.0 0.5)
	(PredicateNode "CapableOf" (stv 2.5245749935e-09 0.949999988079))
	(ListLink
		(ConceptNode "couple" (stv 1.19614360301e-05 0.949999988079))
		(ConceptNode "see_counselor" (stv 2.5245749935e-09 0.949999988079))
	)
)
```

11.
```scheme
/a/[/r/Causes/,/c/en/pass_class/,/c/en/joy/]
	-->
(PredictiveImplicationLink (stv 1.0 0.5)
	(ConceptNode "pass_class" (stv 2.5245749935e-09 0.949999988079))
	(ConceptNode "joy" (stv 3.87219297409e-05 0.949999988079))
)
```
