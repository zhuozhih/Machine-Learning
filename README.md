# Machine-Learning-Higgs-Boson
Group project for machine learning course. 
https://www.kaggle.com/c/higgs-boson/

Quoted from the documentation of the competition:
"The goal of the Challenge is to improve the procedure that produces the selection region. We
provide a training set with signal/background labels and with weights, a test set (without labels
and weights), and a formal objective representing an approximation of the median significance
(AMS) of the counting test. The objective is a function of the weights of selected events. We
expect that significant improvements are possible by re-visiting some of the ad hoc choices in the
standard procedure, or by incorporating the objective function or a surrogate into the classifier
design.

Some details to get started:

all variables are floating point, except PRI_jet_num which is integer
variables prefixed with PRI (for PRImitives) are “raw” quantities about the bunch collision as measured by the detector.
variables prefixed with DER (for DERived) are quantities computed from the primitive features, which were selected by  the physicists of ATLAS
it can happen that for some entries some variables are meaningless or cannot be computed; in this case, their value is −999.0, which is outside the normal range of all variables.


Evaluation

The evaluation metric is the approximate median significance (AMS):

AMS=sqrt(2((s+b+br)log(1+s/(sb+br))−s))
where s,b: unnormalized true positive and false positive rates, respectively,

br=10 is the constant regularization term, 

log is the natural log.

More precisely, let (y1,…,yn)∈{b,s}^n be the vector of true test labels, let (ŷ_1,…,ŷ_n)∈{b,s}^n be the vector of predicted (submitted) test labels, and let (w1,…,wn)∈ ℝ^{+n} be the vector of weights. Then

s=∑w_i 𝟙{yi=s}𝟙{ŷi=s}
and

b=∑w_i 𝟙{yi=b}𝟙{ŷi=s},

where the indicator function 𝟙{A} is 1 if its argument AA is true and 0 otherwise.

For more information on the statistical model and the derivation of the metric, see the technical documentation. We have provided python code for the metric is available from the Data page and a Python starting kit.

Submission Instructions

The submission file format is 

EventId,RankOrder,Class
1,2,b
2,541234,s
3,5,b
4,1,b
5,542456,s
...
Your submission file should have a header row and three columns

EventId is a unique identifier for each event. The list of EventIds must correspond to the exact list of EventIds in test.csv, but the ordering can be arbitrary.
RankOrder is a permutation of the integer list [1,550000]. The higher the rank (larger integer value), the more signal-like is the event. 550000 is the most signal-like event. The largest background rank should be one less than the smallest signal one. Most predictors output a real-valued score for each event in the test set, in which case RankOrder is just the ordering of the test points according to the score. The RankOrder is not used for computing the AMS, but it allows the organizers to compute other metrics (e.g., ROC) related to the classification task, which is not captured entirely by the classification alone.
Class is either "b" or "s", and it indicates if your prediction (ŷ iy^i above in the formal definition) for the event is background or signal. The AMS will be calculated based on the (hidden) weights of events that you mark "s".
