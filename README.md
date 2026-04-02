# ♟️ Onestep Checkmate Prediction

![Python](https://img.shields.io/badge/Python-3.8+-blue?style=flat-square&logo=python)
![OpenCV](https://img.shields.io/badge/OpenCV-4.x-green?style=flat-square&logo=opencv)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=flat-square)

A computer vision system that **reads a real chessboard from an image** and predicts whether Black can deliver **checkmate in one move** — using OpenCV for board detection and a custom-built chess rule engine.

---

## 📌 Problem Statement

Given an image of a chess position, can a program automatically:
1. Detect and extract the chessboard from the image
2. Recognize all pieces on the board
3. Calculate if Black can force checkmate in exactly one move

This project answers all three — without any external chess libraries.

---

## 🎯 How It Works

```
Input Image (chess position)
        ↓
[OpenCV] Chessboard Detection
   - Canny edge detection
   - Contour extraction
   - Perspective transform (warp to 800x800)
        ↓
[OpenCV] Piece Recognition
   - Split board into 64 squares
   - Template matching against piece image library
   - Assign piece codes (e.g. 'wk', 'bp', 'br')
        ↓
[Rule Engine] Chess Logic
   - Generate all legal moves for Black
   - Simulate each move on the board
   - Check if White King is in checkmate
        ↓
Output: "Move e7 TO e8" or "No checkmate in ONE step!"
```

---

## 🧠 Chess Rule Engine

A fully custom rule engine built from scratch in Python — no external chess libraries used.

Supports all piece movement rules:
- **Pawn** — forward movement, diagonal captures, double first move, promotion to Queen/Knight
- **Rook** — horizontal/vertical sliding
- **Bishop** — diagonal sliding
- **Knight** — L-shaped jumps
- **Queen** — combined Rook + Bishop movement
- **King** — one-step in all directions

Also implements:
- **Check detection** — identifies if the White King is under attack
- **Checkmate verification** — confirms no legal escape moves exist
- **Pawn promotion** — tries both Queen and Knight promotions when solving

---

## 🛠️ Tech Stack

| Component | Technology |
|---|---|
| Image processing | OpenCV (cv2) |
| Board detection | Canny Edge Detection + Contour Analysis |
| Perspective correction | Homography / Perspective Transform |
| Piece recognition | Template Matching (TM_CCOEFF_NORMED) |
| Chess logic | Custom Python Rule Engine |
| Numerical operations | NumPy |

---

## 📁 Project Structure

```
Onestep-Checkmate-prediction/
├── script.py           # Chess rule engine + checkmate solver
├── boardToMat.py       # OpenCV board detection + piece recognition
├── image.png           # Sample chess board image (input)
└── chess_pieces/       # Template images for each piece
    ├── wp/             # White Pawn
    ├── wr/             # White Rook
    ├── wn/             # White Knight
    ├── wb/             # White Bishop
    ├── wq/             # White Queen
    ├── wk/             # White King
    ├── bp/             # Black Pawn
    ├── br/             # Black Rook
    ├── bn/             # Black Knight
    ├── bb/             # Black Bishop
    ├── bq/             # Black Queen
    └── bk/             # Black King
```

---

## ⚙️ How to Run

### 1. Clone the repository
```bash
git clone https://github.com/MyadaSathwik/Onestep-Checkmate-prediction.git
cd Onestep-Checkmate-prediction
```

### 2. Install dependencies
```bash
pip install opencv-python numpy
```

### 3. Run with a board image
```bash
python boardToMat.py
```
This reads `image.png`, detects the board, recognizes pieces, and prints the checkmate move.

### 4. Run with a manual board (no image needed)
```python
from script import ChessBoard

board = [
    ['00', '00', '00', '00', '00', '00', '00', '00'],
    ['00', 'bp', '00', '00', '00', '00', '00', '00'],
    ['wk', '00', '00', '00', '00', '00', '00', '00'],
    ['00', '00', '00', 'bb', '00', '00', '00', '00'],
    ['bk', '00', '00', 'bb', '00', '00', '00', '00'],
    ...
]

obj = ChessBoard(board)
print(obj.findMove())  # Output: "Move g7 TO g8"
```

---

## 🔢 Board Representation

Each square is encoded as a 2-character string:

| Code | Meaning |
|---|---|
| `wk` | White King |
| `bq` | Black Queen |
| `wp` | White Pawn |
| `00` | Empty square |

Rows 0–7 map to ranks 8–1; columns 0–7 map to files h–a in standard chess notation.

---

## 🔮 Future Enhancements

- [ ] **Multi-step solver** — extend to find checkmate in N moves
- [ ] **CNN-based piece recognition** — replace template matching with a trained classifier for better accuracy
- [ ] **Live webcam input** — real-time board detection from a camera feed
- [ ] **Web interface** — upload a board image and get the move in browser
- [ ] **FEN notation support** — accept standard chess position strings as input

---

## 👤 Author

**Myada Sathwik and Ande Pavan Kumar**  
B.Tech Information Technology — MLR Institute of Technology, Hyderabad  
📧 myadasathwik14@gmail.com  
🔗 [GitHub](https://github.com/MyadaSathwik)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
