#include <iostream>
#include <fstream>
#include <vector>
#include <string>
#include <cmath>
using namespace std;

void groupAndSaveData() {
    vector<string> filenames = {
        "Kisi-1-Taşikardi.txt", "Kisi-1-Bradikardi.txt", "Kisi-1-Normal.txt",
        "Kisi-2-Taşikardi.txt", "Kisi-2-Bradikardi.txt", "Kisi-2-Normal.txt"
    };

    //Dosya acma
    ofstream tasikardiOutput("Taşikardi-Kişi-1-2-3.txt", ios::out);
    ofstream brakardiOutput("Bradikardi-Kişi-1-2-3.txt", ios::out);
    ofstream normalOutput("Normal-Kişi-1-2-3.txt", ios::out);

    // Dosyalari gruplama ve yeni dosyalara yazma
    for (size_t i = 0; i < filenames.size(); ++i) {
        ifstream inputFile(filenames[i], ios::in);
        if (!inputFile.is_open()) {
            cerr << "Dosya açılamadı: " << filenames[i] << endl;
            continue;
        }
        
        ofstream* outputFile;
        if (filenames[i].find("Taşikardi") != string::npos) {
            outputFile = &tasikardiOutput;
        } else if (filenames[i].find("Bradikardi") != string::npos) {
            outputFile = &brakardiOutput;
        } else {
            outputFile = &normalOutput;
        }

        // Dosya icerigini oku ve yaz
        string line;
        *outputFile << "*******************\n";
        while (getline(inputFile, line)) {
            *outputFile << line << endl;
        }
        inputFile.close();
    }

    // Dosyayı kapat
    tasikardiOutput.close();
    brakardiOutput.close();
    normalOutput.close();
}

int main() {
    // Main kisimda cagirilacak
    groupAndSaveData();

    return 0;
}
