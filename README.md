
# ΑΡΧΙΤΕΚΤΟΝΙΚΗ ΠΡΟΗΓΜΕΝΩΝ ΥΠΟΛΟΓΙΣΤΩΝ


## Εργαστήριο Β' - Ομάδα 14
 
* Παπαδόπουλος Σωτήριος (Α.Ε.Μ. 4822, <swtos@ece.auth.gr>)
* Σαββάογλου Δημήτριος  (Α.Ε.Μ. 9388, <dsavvaog@ece.auth.gr>)

### **3η Εργαστηριακή Άσκηση: Energy‐Delay‐Area Product Optimization**


  Το θέμα της 3ης εργαστηριακής άσκησης είναι η εξοικείωση με τον εξομοιωτή _McPAT_ και η διερεύνηση της βελτιστοποίησης του _Energy-Delay-Product (EDP)_ χρησιμοποιώντας τα δεδομένα της 2ης εργαστηριακής άσκησης.


**ΠΡΟΕΡΓΑΣΙΑ:**

Κατεβάσαμε και κάναμε build το εργαλείο _McPAT_ μαζί με τα προαπαιτούμενα πακέτα.


**ΕΡΩΤΗΜΑΤΑ:**

**Βήμα 1ο**

1)   Dynamic power (δυναμική ισχύς) είναι η ισχύς η οποία καταναλώνεται από το κύκλωμα όταν σε αυτό υπάρχει ροή πληροφορίας από ένα επίπεδο σε ένα άλλο. Αποτελεί το μεγαλύτερο ποσοστό της peak power και είναι συνάρτηση της τάσης παροχής (supply voltage), της συχνότητας μεταγωγής (switching frequency) των τρανζίστορ και του φορτίου που δίνει την έξοδο (output load) του κυκλώματος.     
     Leakage power (ισχύς διαρροής) είναι από την άλλη η ισχύς η οποία καταναλώνεται από το κύκλωμα όταν δεν υπάρχει μεταγωγή στα τρανζίστορ του ολοκληρωμένου, άρα η είσοδος (input) είναι σταθερή. Αποτελεί το υπόλοιπο ποσοστό της peak power και εξαρτάται από τη θερμοκρασία του περιβάλλοντος (ambient temperature), την τάση κατωφλίου (thresold voltage) του ολοκληρωμένου και το συνδυασμό εισόδων (input combination) του ολοκληρωμένου όταν αυτό βρίσκεται σε αδράνεια (steady state). Συγκεκριμένα η leakage power παρουσιάζει εκθετική μεταβολή με τη θερμοκρασία, όπως ισχύει για τα τρανζίστορ που αποτελούν το ολοκληρωμένο.
      Τρέχοντας το McPAT στον επεξεργαστή Xeon λαμβάνουμε dynamic power ίσο με 98.1063 W και leakage power ίσο με 36.8319 W. Αν τρέξω άλλο πρόγραμμα στον ίδιο επεξεργαστή αυτό που θα αλλάξει θα είναι το dynamic power, ανάλογα με την παράμετρο δραστηριότητα (activity) εντός του κυκλώματος κατά την εκτέλεση του προγράμματος. Ο χρόνος εκτέλεσης ενός προγράμματος δεν επηρεάζει ωστόσο την ισχύ διότι η καταναλισκόμενη ισχύς σε ένα κύκλωμα είναι εξ ορισμού ανεξάρτητη του χρόνου λειτουργίας αυτού.

2)   Ο επεξεργαστής των 40 Watt θα καταναλώνει περισσότερη ενέργεια από αυτόν των 4 Watt, οπότε το λογικό είναι να δίνει μικρότερη διάρκεια ζωής μπαταρίας (για συγκεκριμένη χωρητικότητα). Ωστόσο από το αποτέλεσμα της εκτέλεσης του McPAT στο τερματικό οι μόνες πληροφορίες που παίρνουμε αφορούν μεγέθη ισχύος και όχι χρόνου. Για να απαντήσουμε με βεβαιότητα ποιος από τους δύο επεξεργαστές δίνει μεγαλύτερη διάρκεια θα πρέπει να γνωρίζουμε την τάση παροχής (άρα το φορτίο της μπαταρίας) η οποία όμως ορίζεται διαφορετικά από κάθε αρχείο .xml.

3)   Αφενός, τρέχοντας τον επεξεργαστή Xeon παίρνουμε peak power 134.938 W.  Αφετέρου, για τον επεξεργαστή ARM A9 διαβάζουμε 1,74189 W. Με άλλα λόγια ο δεύτερος επεξεργαστής καταναλώνει σημαντικά μικρότερη ισχύ από τον πρώτο, και η μεγάλη διαφορά στην ταχύτητα μεταξύ των δύο επεξεργαστών δεν επαρκεί για να καλύψει την αντίστοιχη διαφορά στην ισχύ, πόσο μάλλον να την αντιστρέψει (λόγος ισχύων ≈ 77.5 > 40). Δεδομένου ότι καταναλισκόμενη ενέργεια = καταναλισκόμενη ισχύς x χρόνος εκτέλεσης, μπορούμε να πούμε με ασφάλεια ότι ο επεξεργαστής Xeon δε μπορεί να είναι πιο αποδοτικός ενεργειακά (energy efficient) από τον ARM A9. 

**Βήμα 2ο**


**ΚΑΤΑΝΑΛΩΣΗ ΕΝΕΡΓΕΙΑΣ:**

**_bzip_:**

L1 d-cache 32KB: 0,068478098 J, EDP = 0,005813517

L1 d-cache 64KB: 0,117778837 J, EDP = 0,009799317

L1 d-cache 128KB: 0,146727741 J, EDP = 0,011998661

L1 d-cache associativity 2: 0,117778837 J, EDP = 0,009799317

L1 d-cache associativity 8: 0,10237201 J, EDP = 0,008440982

L1 d-cache associativity 16: 0,125447468 J, EDP = 0,010320939

L1 i-cache 32KB: 0,117778837 J, EDP = 0,009799317

L1 i-cache 64KB: 0,151461784 J, EDP = 0,012601317

L1 i-cache 128KB: 0,175226695 J, EDP = 0,014578686

L1 i-cache associativity 2: 0,117778837 J, EDP = 0,009799317

L1 i-cache associativity 8: 0,128056592 J, EDP = 0,010655077

L1 i-cache associativity 16: 0,133669832 J, EDP = 0,011121731

L2 cache 1024KB: 0,11895437 J, EDP = 0,010076149

L2 cache 2048KB: 0,117778837 J, EDP = 0,009799317

L2 cache 4096KB: 0,11702195 J, EDP = 0,009571927

L2 cache associativity 8: 0,117778837 J, EDP = 0,009799317

L2 cache associativity 64: 0,118048735 J, EDP = 0,009822481

L2 cache associativity 512: 0,122871161 J, EDP = 0,010224355

cache line size 32 bytes: 0,087025118 J, EDP = 0,008034942

cache line size 64 bytes: 0,117778837 J, EDP = 0,009799317

cache line size 128 bytes: 0,146054552 J, EDP = 0,012043512

Έχουμε βέλτιστο EDP για L1 d-cache 32KB, assoc. 2, L1 i-cache 32KB, assoc. 2, L2 cache 2048KB, assoc. 8, cache line size 64 bytes.

**_mcf_:**

L1 d-cache 32KB: 0,048671009 J, EDP = 0,002865603

L1 d-cache 64KB: 0,084405199 J, EDP = 0,004966064

L1 d-cache 128KB: 0,106505964 J, EDP = 0,006264361

L1 d-cache associativity 2: 0,084405199 J, EDP = 0,004966064

L1 d-cache associativity 8: 0,075900218 J, EDP = 0,004464147

L1 d-cache associativity 16: 0,092354986 J, EDP = 0,005431304

L1 i-cache 32KB: 0,084405199 J, EDP = 0,004966064

L1 i-cache 64KB: 0,105899765 J, EDP = 0,006083836

L1 i-cache 128KB: 0,122267902 J, EDP = 0,007023802

L1 i-cache associativity 2: 0,084405199 J, EDP = 0,004966064

L1 i-cache associativity 4: 0,087192155 J, EDP = 0,005009102

L1 i-cache associativity 16: 0,093609737 J, EDP = 0,005377786

L2 cache 1024KB: 0,084437805 J, EDP = 0,004986559

L2 cache 2048KB: 0,084405199 J, EDP = 0,004966064

L2 cache 4096KB: 0,084781817 J, EDP = 0,004987375

L2 cache associativity 8: 0,084405199 J, EDP = 0,004966064

L2 cache associativity 32: 0,084449764 J, EDP = 0,004968686

L2 cache associativity 128: 0,084731358 J, EDP = 0,004985

cache line size 32 bytes: 0,058598957 J, EDP = 0,003502167

cache line size 64 bytes: 0,084405199 J, EDP = 0,004966064

cache line size 128 bytes: 0,103605073 J, EDP = 0,006089906

Έχουμε βέλτιστο EDP για L1 d-cache 32KB, assoc. 2, L1 i-cache 32KB, assoc. 2, L2 cache 2048KB, assoc. 8, cache line size 64 bytes.

**_hmmer_:**

L1 d-cache 32KB: 0,048029954 J, EDP = 0,002795391

L1 d-cache 64KB: 0,085806495 J, EDP = 0,004984328

L1 d-cache 128KB: 0,108197353 J, EDP = 0,006260082

L1 d-cache associativity 2: 0,085806495 J, EDP = 0,004984328

L1 d-cache associativity 8: 0,075405515 J, EDP = 0,004370353

L1 d-cache associativity 16: 0,094046227 J, EDP = 0,005450637

L1 i-cache 32KB: 0,085806495 J, EDP = 0,004984328

L1 i-cache 64KB: 0,109312125 J, EDP = 0,006348848

L1 i-cache 128KB: 0,125896754 J, EDP = 0,007311832

L1 i-cache associativity 2: 0,085806495 J, EDP = 0,004984328

L1 i-cache associativity 8: 0,092966812 J, EDP = 0,005399512

L1 i-cache associativity 16: 0,09688802 J, EDP = 0,005627256

L2 cache 1024KB: 0,085646319 J, EDP = 0,004975023

L2 cache 2048KB: 0,085806495 J, EDP = 0,004984328

L2 cache 4096KB: 0,086134811 J, EDP = 0,005003399

L2 cache associativity 8: 0,085806495 J, EDP = 0,004984328

L2 cache associativity 32: 0,085847377 J, EDP = 0,004986702

L2 cache associativity 128: 0,086111116 J, EDP = 0,005002023

cache line size 32 bytes: 0,058428272 J, EDP = 0,00342787

cache line size 64 bytes: 0,085806495 J, EDP = 0,004984328

cache line size 128 bytes: 0,104766106 J, EDP = 0,006065329

Έχουμε βέλτιστο EDP για L1 d-cache 32KB, assoc. 2, L1 i-cache 32KB, assoc. 2, L2 cache 2048KB, assoc. 8, cache line size 64 bytes.

**_sjeng_:**

L1 d-cache 32KB: 0,386138821 J, EDP = 0,199317137

L1 d-cache 64KB: 0,628767703 J, EDP = 0,324575547

L1 d-cache 128KB: 0,792055138 J, EDP = 0,408864407

L1 d-cache associativity 2: 0,628767703 J, EDP = 0,324575547

L1 d-cache associativity 4: 0,533365012 J, EDP = 0,275331553

L1 d-cache associativity 8: 0,604569608 J, EDP = 0,312083063

L1 i-cache 32KB: 0,628767703 J, EDP = 0,324575547

L1 i-cache 64KB: 0,83759863 J, EDP = 0,432277952

L1 i-cache 128KB: 0,985002454 J, EDP = 0,508350902

L1 i-cache associativity 2: 0,628767703 J, EDP = 0,324575547

L1 i-cache associativity 4: 0,692474894 J, EDP = 0,357450693

L1 i-cache associativity 8: 0,727211637 J, EDP = 0,375320471

L2 cache 1024KB: 0,626310474 J, EDP = 0,32337725

L2 cache 2048KB: 0,628767703 J, EDP = 0,324575547

L2 cache 4096KB: 0,63280633 J, EDP = 0,326552113

L2 cache associativity 2: 0,628656406 J, EDP = 0,324509922

L2 cache associativity 8: 0,628767703 J, EDP = 0,324575547

L2 cache associativity 32: 0,630517625 J, EDP = 0,325306111

cache line size 32 bytes: 0,745684854 J, EDP = 0,661623801

cache line size 64 bytes: 0,628767703 J, EDP = 0,324575547

cache line size 128 bytes: 0,511235907 J, EDP = 0,174674995

Έχουμε βέλτιστο EDP για L1 d-cache 64KB, assoc. 2, L1 i-cache 32KB, assoc. 2, L2 cache 2048KB, assoc. 8, cache line size 128 bytes.

**_libm_:**

L1 d-cache 32KB: 0,133558339 J, EDP = 0,023378987

L1 d-cache 64KB: 0,221812557 J, EDP = 0,038827623

L1 d-cache 128KB: 0,279492756 J, EDP = 0,048924369

L1 d-cache associativity 2: 0,221812557 J, EDP = 0,038827623

L1 d-cache associativity 8: 0,185370207 J, EDP = 0,032448499

L1 d-cache associativity 16: 0,215054831 J, EDP = 0,037644703

L1 i-cache 32KB: 0,221812557 J, EDP = 0,038827623

L1 i-cache 64KB: 0,292693446 J, EDP = 0,05123628

L1 i-cache 128KB: 0,342691495 J, EDP = 0,059988489

L1 i-cache associativity 2: 0,221812557 J, EDP = 0,038827623

L1 i-cache associativity 8: 0,243427469 J, EDP = 0,042612222

L1 i-cache associativity 16: 0,255244512 J, EDP = 0,044680807

L2 cache 1024KB: 0,221141365 J, EDP = 0,038733574

L2 cache 2048KB: 0,221812557 J, EDP = 0,038827623

L2 cache 4096KB: 0,222888121 J, EDP = 0,038963964

L2 cache associativity 8: 0,221812557 J, EDP = 0,038827623

L2 cache associativity 64: 0,222423405 J, EDP = 0,03893455

L2 cache associativity 512: 0,233269062 J, EDP = 0,040771

cache line size 32 bytes: 0,240717251 J, EDP = 0,067479545

cache line size 64 bytes: 0,221812557 J, EDP = 0,038827623

cache line size 128 bytes: 0,202066544 J, EDP = 0,026082345

Έχουμε βέλτιστο EDP για L1 d-cache 32KB, assoc. 2, L1 i-cache 32KB, assoc. 2, L2 cache 2048KB, assoc. 8, cache line size 64 bytes.
















**Ακολουθούν τα διαγράμματα που δείχνουν την επίδραση κάθε παράγοντα στο peak power:**

![Pie Charts](/bzip.png) ![Pie Charts](/mcf.png)
![Pie Charts](/hmmer.png) ![Pie Charts](/sjeng.png)
![Pie Charts](/lbm.png)
















