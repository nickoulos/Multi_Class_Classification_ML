# Multi_Class_Classification_MachineLearning
(AUEB 2019 subject: "Data Mining") Machine Learning project for Kaggle competition: The case of flight passengers prediction

### Εισαγωγή

Στην εργασία του μαθήματος, κληθήκαμε να υλοποιήσουμε έναν αλγόριθμο μηχανικής μάθησης που να εκπαιδεύεται πάνω σε ένα dataset (train.csv) έτσι ώστε να προβλέπει την στήλη PAX σε καινούρια datasets (της μορφής test.csv).Στο συγκεκριμένο προβλήμα δοκιμάσαμε πέντε διαφορετικές προσεγγίσεις με τους αλγόριθμους:**Logistic Regression , Decision Tree , Random Forest , k-nearest neighbors και Neural Networks.**

### Dimensionality Reduction and Pre-processing

Στους περισσότερους αλγόριθμους που υλοποιήσαμε δεν δώσαμε ως όρισμα το default train dataset διότι πολλές πληροφορίες που περιείχε δεν συνέβαλαν στην δημιουργία ορθών συμπερασμάτων και προβλέψεων ή προκαλούσαν πρόβλημα στην κωδικοποίηση.Από τα αρχικά δεδομένα, δημιουργήσαμε άλλα συνδυάζοντας τα πρώτα και στη συνέχεια αφαιρέσαμε όσα προκαλούσαν "θόρυβο" ή δεν συνέβαλαν στην ακρίβεια.
Πιο συγκεκριμένα,πάνω από πολλά κομμάτια του κώδικα, (βρίσκεται παρακάτω) υπάρχει περιγραφή για την ακριβή τροποποίηση/μετατροπή που υπέστησαν τα δεδομένα.
Σαν πρώτη προσπάθεια για ανάλυση των δεδομένων αφου δημιουργήσαμε μια μεταβλητή με τις μέρες τις βδομάδας, προσπαθήσαμε να βρούμε την σχέση της μεταβλητής αυτης για τις διάφορες τιμές της μεταβλητής PAX. 
Μέσω του παρακάτω σχεδιαγράμματος παρατηήσαμε ότι το Σαββατο φαινεται οτι αλλαζουν πολυ οι κατανομες στην μεταβλτητη PAX. Έτσι καταλήξαμε στο συμπέρασμα οτι η δημιουργια της μεταβλητης μερες της εβδομαδας ειναι σημαντικη. 

![image.png](:image.png)

### Logistic Regression

Στην πρώτη προσέγγιση μας, με τον αλγόριθμο **Logistic Regression** κάναμε αρκέτες μετατροπές στην μορφή των δεδομένων εκπαίδευσης (df_train), αφαιρώντας στήλες με σκοπό την εύρεση της πιο αποτελεσματικής δομής.Μετατρέψαμε τις αλφαριθμητικές στήλες Departure,Arrival σε ακεραίους με την χρήση του Label Encoder, και έπειτα χρησιμοποιήσαμε τον One Hot encoder στον πίνακα με τα δεδομένα.Μετά από αρκετές δοκιμές  παρατηρήσαμε ότι η καλύτερη ακρίβεια έφτανε στο 0.37 και γινόταν με τη χρήση μόνο των στηλών Arrival και Departure.Δεν δημιουργήσαμε περαιτέρω δεδομένα στον συγκεκριμένο αλγόριθμο γιατί δεν βλέπαμε μεγάλη βελτίωση στο αποτέλεσμα.Ο χρόνος εκπαίδευσης δεν ξεπερνούσε τα 2 δευτερόλεπτα.

### K-Nearest Neighbors

Στην συνέχεια επιλέξαμε να χρησιμποιήσουμε τον KNN(K-Nearest Neighbors) καθώς είναι ένας απλός στην υλοποίηση αλγόριθμος. Ωστόσο παρατηρήσαμε ότι δεν λειτουργεί αποτελεσματικά με πολλές διαστάσεις και στην περίπτωση μας που είχαμε να επεξεργαστούμε πολλές μεταβλητές δεν έδινε καλά αποτελέσματα. Για την υλοποίηση του KNN χρησιμοποιήσαμε την βιβλιοθήκη του scikit-learn και η ακρίβεια που πετύχαμε έφτανε περίπου το 0.44

### Decision Tree
Ο τρίτος αλγόριθμος που χρησιμοποιήσαμε ήταν τα **Decision Trees** τα οποία γνωρίζουμε πως ταιριάζουν σε προβλήματα κατηγοριοποίησης.Το decision tree που υλοποιήσαμε έγινε με το DecisionTreeClassifier του scikit-learn και η μέγιστη ακρίβεια η οποία επιτεύχθηκε ήταν λίγο πάνω από το 0.42 (0.42352).Παρατηρήσαμε ό,τι χρησιμοποιώντας πολλές στήλες του πίνακα εκπαίδευσης, η απόδοση δεν βελτιωνόταν, γεγονός που πιστεύουμε ότι οφείλεται στο ότι ήταν πολλά τα features για τον μέγεθος του dataset για το decision tree.

### Random Forest
Για αυτό δοκιμάσαμε στην συνέχεια τον **Random Forest** αλγόριθμο του scikit-learn (RandomForestClassifier) και δημιουργήσαμε 300 estimators-decision trees με max depth 12, αφού μετά από δοκιμές οι συγκεκριμένοι αριθμοί έδιναν το καλύτερο αποτέλεσμα.
Με το Random Forest δυστυχώς δεν είχαμε τη βελτίωση στην ακρίβεια που περιμέναμε (το μέγιστο ήταν κοντά στο 0.44) με αποτέλεσμα να στραφούμε σε άλλους αλγορίθμους.

### Keras Neural Network

Επίσης, υλοποιήσαμε νευρωνικά δίκτυα μέσω του keras. Βρήκαμε ότι είναι μια πολύ καλή βιβλιοθήκη για αρχάριους στον τομέα των νευρωνικών δικτύων, αρκετά ευέλικτη και κατανοητή. Για να χτίσουμε το νευρωνικό δίκτυο αρχικα καταλήξαμε ότι 4 layers είναι αρκετά. Μετά από κάθε layer εφαρμόζαμε Dropout καθώς βοηθάει να αποφύγουμε το overfitting. Καταλήξαμε οτι το δίκτυο αποδίδει καλά σε χρόνο και accuracy με 500 νευρώνες στα hidden layers και 8 στο output layer, ενώ επίσης παρατηρήσαμε οτι ενώ αυξάναμε τα epochs αυξανόταν και το accuracy με πιο αργο ρυθμο. Με τις κατάλληλες παραμέτρους το νευρωνικό δίκτυο χρειαζόταν 1 δευτερόλεπτο για κάθε epoch. Ωστόσο η μέγιστη απόδοση που πετύχαμε έφτανε το 0.50 . 

### Κώδικας


Ο κώδικας που ακολουθεί, είναι ο τελικός κώδικας που οδήγησε στο βέλτιστο αποτέλεσμα προβλέψεων που επιτύχαμε(0.51347).
Είναι υλοποιημένος με **Neural Networks** του scikit-learn με τον Multi-layer Perceptron, **MLPClassifier**, στο τροποποιημένο αρχικό **train dataset**:

