#include <iostream>
#include <vector>
#include <string>

using namespace std;

// Function to simulate vulnerability scanning
void scanURL(const string& url) {
    cout << "\nScanning: " << url << endl;

    if (url.find("'") != string::npos || url.find("OR 1=1") != string::npos) {
        cout << "[!] Possible SQL Injection detected\n";
    } 
    else if (url.find("<script>") != string::npos) {
        cout << "[!] Possible XSS detected\n";
    } 
    else if (url.find("id=") != string::npos) {
        cout << "[!] Check for IDOR vulnerability\n";
    } 
    else {
        cout << "[+] No obvious issues found\n";
    }
}

int main() {
    vector<string> urls;
    int n;

    cout << "Enter number of URLs to scan: ";
    cin >> n;
    cin.ignore();

    for (int i = 0; i < n; i++) {
        string url;
        cout << "Enter URL " << i + 1 << ": ";
        getline(cin, url);
        urls.push_back(url);
    }

    cout << "\n--- Scan Results ---\n";
    for (const auto& url : urls) {
        scanURL(url);
    }

    return 0;
}
