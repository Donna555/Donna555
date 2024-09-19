#include <QApplication>
#include <QWidget>
#include <QVBoxLayout>
#include <QPushButton>
#include <QComboBox>
#include <QLabel>

class TaxiApp : public QWidget {
public:
    TaxiApp(QWidget *parent = nullptr) : QWidget(parent) {
        // Nastavenie základného layoutu
        QVBoxLayout *layout = new QVBoxLayout(this);

        // Nadpis
        QLabel *title = new QLabel("Fiktívna Taxi Aplikácia", this);
        title->setAlignment(Qt::AlignCenter);
        layout->addWidget(title);

        // Výber typu taxíka
        QLabel *selectTaxiLabel = new QLabel("Vyberte typ taxíka:", this);
        layout->addWidget(selectTaxiLabel);

        QComboBox *taxiType = new QComboBox(this);
        taxiType->addItem("Economy");
        taxiType->addItem("Comfort");
        taxiType->addItem("Luxury");
        layout->addWidget(taxiType);

        // Zadajte svoju polohu
        QLabel *locationLabel = new QLabel("Zadajte svoju polohu:", this);
        layout->addWidget(locationLabel);

        QLabel *locationPlaceholder = new QLabel("Fiktívna poloha", this);
        layout->addWidget(locationPlaceholder);

        // Tlačidlo na objednanie taxíka
        QPushButton *orderButton = new QPushButton("Objednať taxík", this);
        layout->addWidget(orderButton);

        // Informácia o potvrdení
        QLabel *confirmationLabel = new QLabel("", this);
        layout->addWidget(confirmationLabel);

        // Pripojenie tlačidla na objednanie k funkcii
        connect(orderButton, &QPushButton::clicked, [confirmationLabel, taxiType]() {
            QString selectedTaxi = taxiType->currentText();
            confirmationLabel->setText("Objednali ste " + selectedTaxi + " taxík.");
        });

        setLayout(layout);
        setWindowTitle("Fiktívna Taxi Aplikácia");
    }
};

int main(int argc, char *argv[]) {
    QApplication app(argc, argv);

    TaxiApp window;
    window.resize(300, 200);
    window.show();

    return app.exec();
}
