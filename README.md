

import Foundation

func readSudokuFromFile(fileName: String) -> [[Int]]? {
    guard let fileURL = Bundle.main.url(forResource: fileName, withExtension: "txt") else {
        print("File not found")
        return nil
    }
    
    do {
        let contents = try String(contentsOf: fileURL, encoding: .utf8)
        let rows = contents.components(separatedBy: .newlines)
        var sudoku: [[Int]] = []
        
        for row in rows {
            if row.isEmpty { continue }
            let digits = row.compactMap { Int(String($0)) }
            if digits.count == 9 {
                sudoku.append(digits)
            }
        }
        
        if sudoku.count == 9 {
            return sudoku
        } else {
            print("Invalid Sudoku format")
            return nil
        }
    } catch {
        print("Error reading file: \(error)")
        return nil
    }
}

func displaySudoku(_ sudoku: [[Int]]) {
    for (index, row) in sudoku.enumerated() {
        if index % 3 == 0 && index != 0 {
            print("- - - - - - - - - - - -")
        }
        for (colIndex, num) in row.enumerated() {
            if colIndex % 3 == 0 && colIndex != 0 {
                print("| ", terminator: "")
            }
            if num == 0 {
                print(". ", terminator: "")
            } else {
                print("\(num) ", terminator: "")
            }
        }
        print()
    }
}

// Usage
if let sudoku = readSudokuFromFile(fileName: "sudoku") {
    displaySudoku(sudoku)
} else {
    print("Failed to read Sudoku puzzle")
}

//learned some from ai
