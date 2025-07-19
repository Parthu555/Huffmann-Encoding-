# Huffmann-Encoding-
A modern, interactive web application that demonstrates Huffman coding for lossless data compression. Built with vanilla JavaScript and featuring a beautiful, responsive UI.
🌟 Features

Lossless Compression: Perfect reconstruction of original data
Interactive Visualization: See the Huffman tree and character codes
Real-time Statistics: Compression ratios, file sizes, and unique characters
Drag & Drop Interface: Easy file uploading
Modern UI: Glassmorphism design with smooth animations
Progress Tracking: Visual feedback during compression/decompression
Download Support: Save compressed files and decompress them

🚀 How It Works
Huffman Algorithm Steps:

Frequency Analysis: Count character occurrences in the input text
Build Min-Heap: Create nodes for each character with their frequencies
Construct Tree: Merge nodes with lowest frequencies until one root remains
Generate Codes: Assign binary codes (left=0, right=1) to each character
Encode: Replace characters with their binary codes
Compress: Store the encoded data with the tree structure

Algorithm Complexity:

Time Complexity: O(n log n) where n is the number of unique characters
Space Complexity: O(n) for storing the tree and codes

📁 File Structure
huffman-compressor/
├── index.html          # Main application file
├── README.md           # This file
├── examples/           # Sample files for testing
│   ├── sample.txt
│   ├── lorem.txt
│   └── code.js
└── docs/              # Documentation
    ├── algorithm.md
    └── api.md
🔧 Usage
Web Application

Open index.html in a modern web browser
Select or drag-drop a text file
Click "Compress File" to encode using Huffman algorithm
View compression statistics and tree visualization
Download the compressed file (.huffman format)
Use "Decompress File" to restore original content

Core JavaScript Classes
javascript// Initialize Huffman encoder
const encoder = new HuffmanEncoder();

// Compress text
const text = "Hello, World!";
const result = encoder.encode(text);
console.log('Encoded:', result.encoded);
console.log('Codes:', result.codes);

// Decompress
const decoded = encoder.decode(result.encoded, result.tree);
console.log('Decoded:', decoded);
🧮 Key Code Snippets
Building Frequency Table
javascriptbuildFrequencyTable(text) {
    const freq = {};
    for (let char of text) {
        freq[char] = (freq[char] || 0) + 1;
    }
    return freq;
}
Constructing Huffman Tree
javascriptbuildHuffmanTree(frequencies) {
    const heap = Object.entries(frequencies)
        .map(([char, freq]) => new HuffmanNode(char, freq))
        .sort((a, b) => a.freq - b.freq);

    while (heap.length > 1) {
        const left = heap.shift();
        const right = heap.shift();
        const merged = new HuffmanNode(null, left.freq + right.freq, left, right);
        
        // Insert in sorted position
        let inserted = false;
        for (let i = 0; i < heap.length; i++) {
            if (merged.freq <= heap[i].freq) {
                heap.splice(i, 0, merged);
                inserted = true;
                break;
            }
        }
        if (!inserted) heap.push(merged);
    }
    return heap[0];
}
Generating Binary Codes
javascriptgenerateCodes(node, code = '', codes = {}) {
    if (node.char !== null) {
        codes[node.char] = code || '0'; // Handle single character
        return codes;
    }
    
    if (node.left) this.generateCodes(node.left, code + '0', codes);
    if (node.right) this.generateCodes(node.right, code + '1', codes);
    
    return codes;
}
📊 Performance Examples
File TypeOriginal SizeCompressed SizeCompression RatioPlain Text1000 bytes~600 bytes~40% reductionCode Files2000 bytes~1200 bytes~40% reductionRepetitive Text1500 bytes~300 bytes~80% reduction
🛠️ Installation & Setup
bash# Clone the repository
git clone https://github.com/yourusername/huffman-compressor.git

# Navigate to project directory
cd huffman-compressor

# Open in browser (no build required!)
open index.html
# OR serve with any static server:
python -m http.server 8000
# OR
npx serve .
🔍 Testing
Test with various file types:

Plain text: Lorem ipsum, articles, stories
Code files: JavaScript, HTML, CSS, JSON
Structured data: XML, configuration files
Repetitive content: Log files, data exports

🎯 Optimization Tips

Best Results: Files with repeated characters/patterns
Poor Results: Already compressed files (images, videos, archives)
Ideal Use Cases: Text files, source code, configuration files
File Size: Works best with files > 1KB for meaningful compression

🤝 Contributing

Fork the repository
Create feature branch: git checkout -b feature/amazing-feature
Commit changes: git commit -m 'Add amazing feature'
Push to branch: git push origin feature/amazing-feature
Open a Pull Request

📚 Educational Value
This implementation demonstrates:

Greedy Algorithms: Huffman coding is a classic greedy approach
Tree Data Structures: Binary trees and traversal
Priority Queues: Min-heap implementation
File I/O: Browser File API usage
Data Visualization: Interactive tree display

📜 License
MIT License - see LICENSE file for details
🔗 References

Huffman Coding - Wikipedia
Data Compression Techniques
Information Theory Basics

🏆 Acknowledgments

David A. Huffman - Creator of Huffman coding (1952)
Claude Shannon - Information theory foundations
Modern web APIs for file handling capabilities

🔧 Testing & Setup Commands
Create Test Files:
bash# Create a simple test file
echo "Hello World! This is a test of Huffman encoding compression." > test.txt

# Create a file with repetitive patterns (great for Huffman)
echo "AAAAAABBBBBBCCCCCCDDDDDDEEEEEEffffff" > repetitive.txt

# Create a larger text file with mixed content
cat << 'EOF' > sample.txt
The quick brown fox jumps over the lazy dog.
Pack my box with five dozen liquor jugs.
How razorback-jumping frogs can level six piqued gymnasts!
Waltz, bad nymph, for quick jigs vex.
EOF

# Generate Lorem Ipsum for testing
curl -s "https://loremipsum.io/generator/?n=10&t=p" -o lorem.txt
File Size Analysis:
bash# Check file sizes before compression
ls -lh *.txt

# Display file content and character count
wc -c test.txt
wc -w test.txt
wc -l test.txt

# Show unique character count
cat test.txt | fold -w1 | sort | uniq -c | sort -nr

# Calculate character frequency
cat test.txt | fold -w1 | grep -v '^$' | sort | uniq -c | sort -nr
📁 Project Structure Commands
Initialize Project:
bash# Create project directory
mkdir huffman-compressor
cd huffman-compressor

# Initialize git repository
git init

# Create directory structure
mkdir examples docs tests
mkdir -p src/{js,css}

# Create example files
echo "Sample text for compression testing" > examples/sample.txt
echo "# Algorithm Documentation" > docs/algorithm.md
Set up development environment:
bash# Serve locally with Python
python3 -m http.server 8080
# Open http://localhost:8080

# OR use Node.js serve
npx serve . -p 8080

# OR use PHP built-in server
php -S localhost:8080
🧪 Testing Different File Types
Create Various Test Files:
bash# JSON file (structured data)
cat << 'EOF' > examples/data.json
{
  "users": [
    {"name": "Alice", "age": 30, "city": "New York"},
    {"name": "Bob", "age": 25, "city": "Los Angeles"},
    {"name": "Charlie", "age": 35, "city": "Chicago"}
  ]
}
EOF

# JavaScript code file
cat << 'EOF' > examples/code.js
function fibonacci(n) {
    if (n <= 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}

const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map(x => x * 2);
console.log(doubled);
EOF

# CSS file with repetitive patterns
cat << 'EOF' > examples/styles.css
.container { margin: 0; padding: 0; }
.header { margin: 10px; padding: 5px; }
.footer { margin: 10px; padding: 5px; }
.sidebar { margin: 15px; padding: 8px; }
EOF

# HTML file
cat << 'EOF' > examples/page.html
<!DOCTYPE html>
<html><head><title>Test</title></head>
<body><h1>Hello World</h1><p>This is a test page.</p></body></html>
EOF
📊 Performance Benchmarking
File Analysis Commands:
bash# Compare file sizes and calculate compression ratios
analyze_compression() {
    original_size=$(wc -c < "$1")
    compressed_size=$(wc -c < "$1.huffman")
    ratio=$(echo "scale=2; (1 - $compressed_size/$original_size) * 100" | bc)
    echo "File: $1"
    echo "Original: $original_size bytes"
    echo "Compressed: $compressed_size bytes" 
    echo "Compression: $ratio%"
    echo "---"
}

# Use the function
analyze_compression test.txt
analyze_compression examples/code.js
Batch Testing:
bash# Test multiple files
for file in examples/*.txt examples/*.js examples/*.json; do
    if [ -f "$file" ]; then
        echo "Testing: $file"
        # You would open the web app and test each file
        ls -lh "$file"
    fi
done

# Create a comprehensive test report
echo "Huffman Compression Test Report" > test_report.txt
echo "Generated: $(date)" >> test_report.txt
echo "=================================" >> test_report.txt

for file in examples/*; do
    if [ -f "$file" ]; then
        size=$(wc -c < "$file")
        chars=$(cat "$file" | wc -c)
        unique=$(cat "$file" | fold -w1 | sort -u | wc -l)
        echo "File: $(basename $file)" >> test_report.txt
        echo "Size: $size bytes" >> test_report.txt
        echo "Unique chars: $unique" >> test_report.txt
        echo "---" >> test_report.txt
    fi
done
🔄 Git Workflow Commands
Repository Management:
bash# Add all files
git add .

# Commit with descriptive message
git commit -m "feat: Add Huffman encoding compressor with tree visualization"

# Create and push to GitHub
git branch -M main
git remote add origin https://github.com/yourusername/huffman-compressor.git
git push -u origin main

# Create feature branches
git checkout -b feature/better-ui
git checkout -b feature/file-formats
git checkout -b feature/performance-optimization

# Tag releases
git tag -a v1.0.0 -m "Initial release of Huffman compressor"
git push origin v1.0.0
🧪 Advanced Testing Commands
Memory and Performance Testing:
bash# Create large test files
head -c 1MB /dev/urandom | base64 > large_random.txt
seq 1 10000 > numbers.txt
yes "Hello World!" | head -1000 > repetitive_large.txt

# Monitor memory usage (macOS/Linux)
top -p $(pgrep -f "python3 -m http.server")

# Time the operations (theoretical - for command line version)
time ./huffman_compress test.txt
Character Frequency Analysis:
bash# Analyze character patterns
frequency_analysis() {
    echo "Character frequency analysis for: $1"
    cat "$1" | fold -w1 | grep -v '^$' | sort | uniq -c | sort -nr | head -10
    echo "Total characters: $(cat "$1" | wc -c)"
    echo "Unique characters: $(cat "$1" | fold -w1 | sort -u | wc -l)"
}

frequency_analysis test.txt
frequency_analysis examples/repetitive.txt
🌐 Web Server Commands
Different Server Options:
bash# Python 3
python3 -m http.server 8000 --bind 127.0.0.1

# Python 2 (legacy)
python2 -m SimpleHTTPServer 8000

# Node.js with live reload
npx live-server --port=8000 --open=/index.html

# PHP
php -S localhost:8000 -t .

# Ruby
ruby -run -e httpd . -p 8000

# Using Docker
echo "FROM nginx:alpine
COPY . /usr/share/nginx/html" > Dockerfile

docker build -t huffman-compressor .
docker run -p 8080:80 huffman-compressor
THANKYOU-
