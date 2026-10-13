# Acceptance criteria — TakeMeter

Five criteria that say what "working" means for this classifier, written in
unit 5 **before** anything was trained.

**All five are yours this time.** None are given. You've had two projects of
practice.

An acceptance criterion names a number. *"The model is accurate"* is an
opinion. *"Every label has an F1 of at least 0.60 on the held-out set"* is a
criterion.

Under each, write a sentence or two on **why that number**. A reason that says
something about your data or your taxonomy earns credit — *"I picked 0.60 F1
for `reaction` because it's my smallest label and I only have about 50
examples of it"*. A reason that could be attached to any project does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## Pick numbers you can defend

Not numbers that sound impressive. Three labels means a coin-flip guesser gets
about 33%, so a target of 0.40 is barely a target. Your number should sit
somewhere you'd honestly call useful.

**Cover at least three of these five areas.** They're here as prompts, not as a
form to fill in — a criterion that fits none of them is fine if it names a
number.

| Area | A question it could answer |
|---|---|
| Overall accuracy | How often does it need to be right to be worth using? |
| Per-label performance | Is one label allowed to be much worse than the others? |
| Balance | How lopsided can your label counts get before it's a problem? |
| Consistency | If someone else labelled the same posts, how often should you agree? |
| Confidence | Should a confident prediction be right more often than an unsure one? |

Two things worth knowing before you pick numbers, because both will affect
whether you hit them:

- **Your smallest label will have the jumpiest score.** If a label has 50
  examples, about 8 land in the test split. An F1 computed on 8 examples moves
  a lot between seeds. A target for that label should be looser than one for
  your biggest label, and saying so is a good reason.
- **Unit 6 tests across three seeds, and the target has to hold across all
  three.** A target of 0.65 against results of 0.71, 0.62, 0.68 is a **miss**.
  Pick with that in mind — it is stricter than it first sounds.

---

## 1. Overall accuracy is at least 0.70 on the held-out set.

The model should be correct on at least 70% of held-out posts.

**Why this target:**

With three balanced labels, a random guesser gets about 33% accuracy, so 0.70 is far above chance and still realistic for a small but well-defined classification task. In a dataset where each label is clearly distinct and the boundary rules are concrete, 70% is a level where the classifier is genuinely useful rather than just marginally better than guessing.

---

## 2. Macro F1 is at least 0.65.

The average F1 across the three labels is at least 0.65.

**Why this target:**

Macro F1 treats all labels equally, so it protects against a model that only does well on the biggest or easiest class. Because the task is three-way classification with reasonably balanced labels, 0.65 is a strong but still achievable target for the overall quality of the classifier.

---

## 3. Every label has an F1 of at least 0.60 on the held-out set.

Each of `analysis`, `hot_take`, and `reaction` gets at least 0.60 F1.

**Why this target:**

A model is not acceptable if it only works on one label while missing another. The dataset is small enough that a single label can have only a few posts in the test split, so I am giving the weakest label a looser threshold than the overall accuracy target; 0.60 still means each class is performing at a usable level without being an easy standard to hit.

---

## 4. Accuracy stays within 0.10 across the three seeds.

The held-out accuracy should move by no more than 0.10 from seed to seed.

**Why this target:**

The notebook explicitly warns that a small or lopsided corpus can make scores swing a lot when the split changes. Since the classifier is evaluated on three different 70/15/15 splits, a spread wider than 10 points would mean the score is too dependent on luck rather than a stable pattern in the data.

---

## 5. The most-confident third of predictions is at least 0.15 more accurate than the least-confident third.

The accuracy of the top-confidence third of predictions is at least 0.15 higher than the bottom-confidence third.

**Why this target:**

Confidence only matters if the model is more often right when it feels sure. On this task, a 15-point difference between the confident and uncertain predictions is a meaningful signal that the model is calibrating rather than just guessing; if the confident predictions are not meaningfully better, then the confidence score is not useful.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 6 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath, like this:

         ## 2. Every label performs acceptably

         The model performs well on all labels.

         **Why this target:** ...

         > **Revised in unit 6:** Every label has an F1 of at least 0.60 on
         > the held-out set.
         >
         > **Why revised:** "performs well" gave me nothing to check. I
         > couldn't produce a verdict from it at all.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "Overall accuracy of at least 0.65" → "at least 0.55", because
            0.65 turned out to be optimistic for 200 examples.

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.
     ───────────────────────────────────────────────────────────────────────── -->
