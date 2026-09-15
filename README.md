# Ex05 Image Carousel
## Date:

## AIM
To create a Image Carousel using React 

## ALGORITHM
### STEP 1 Initial Setup:
Input: A list of images to display in the carousel.

Output: A component displaying the images with navigation controls (e.g., next/previous buttons).

### Step 2 State Management:
Use a state variable (currentIndex) to track the index of the current image displayed.

The carousel starts with the first image, so initialize currentIndex to 0.

### Step 3 Navigation Controls:
Next Image: When the "Next" button is clicked, increment currentIndex.

If currentIndex is at the end of the image list (last image), loop back to the first image using modulo:
currentIndex = (currentIndex + 1) % images.length;

Previous Image: When the "Previous" button is clicked, decrement currentIndex.

If currentIndex is at the beginning (first image), loop back to the last image:
currentIndex = (currentIndex - 1 + images.length) % images.length;

### Step 4 Displaying the Image:
The currentIndex determines which image is displayed.

Using the currentIndex, display the corresponding image from the images list.

### Step 5 Auto-Rotation:
Set an interval to automatically change the image after a set amount of time (e.g., 3 seconds).

Use setInterval to call the nextImage() function at regular intervals.

Clean up the interval when the component unmounts using clearInterval to prevent memory leaks.

## PROGRAM
App.jsx
```
import { useState, useEffect } from "react";
import "./App.css";

function App() {
  const images = [
    "https://images.unsplash.com/photo-1565299624946-b28f40a0ae38?w=1000",
    "https://images.unsplash.com/photo-1565958011703-44f9829ba187?w=1000",
    "https://images.unsplash.com/photo-1473093295043-cdd812d0e601?w=1000",
    "https://images.unsplash.com/photo-1546069901-ba9599a7e63c?w=1000",
    "https://images.unsplash.com/photo-1551024506-0bccd828d307?w=1000"
  ];

  const [currentIndex, setCurrentIndex] = useState(0);

  function nextImage() {
    setCurrentIndex((current) =>
      current === images.length - 1
        ? 0
        : current + 1
    );
  }

  function previousImage() {
    setCurrentIndex((current) =>
      current === 0
        ? images.length - 1
        : current - 1
    );
  }

  useEffect(() => {
    const interval = setInterval(() => {
      nextImage();
    }, 3000);

    return () => clearInterval(interval);
  }, []);

  return (
    <div className="carousel-container">
      <h1>🍴 Food Image Carousel</h1>

      <div className="carousel">
        <img
          src={images[currentIndex]}
          alt={`Food ${currentIndex + 1}`}
        />

        <button
          className="prev"
          onClick={previousImage}
        >
          ❮
        </button>

        <button
          className="next"
          onClick={nextImage}
        >
          ❯
        </button>
      </div>

      <div className="dots">
        {images.map((_, index) => (
          <button
            key={index}
            className={
              currentIndex === index
                ? "dot active"
                : "dot"
            }
            onClick={() => setCurrentIndex(index)}
          />
        ))}
      </div>

      <p>
        Image {currentIndex + 1} of {images.length}
      </p>
    </div>
  );
}

export default App;
```
App.css
```
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f5f5f5;
}

.carousel-container {
  min-height: 100vh;

  display: flex;
  flex-direction: column;

  align-items: center;
  justify-content: center;

  padding: 30px;
}

.carousel-container h1 {
  margin-bottom: 30px;

  font-size: 40px;
  color: #222;
}

.carousel {
  width: 800px;
  height: 450px;

  max-width: 90vw;

  position: relative;
  overflow: hidden;

  border-radius: 20px;

  background: #ddd;

  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.2);
}

.carousel img {
  width: 100%;
  height: 100%;

  display: block;

  object-fit: cover;
}

/* Previous and Next Buttons */

.prev,
.next {
  position: absolute;

  top: 50%;
  transform: translateY(-50%);

  width: 55px;
  height: 55px;

  border: none;
  border-radius: 50%;

  background: rgba(0, 0, 0, 0.7);
  color: white;

  font-size: 25px;
  cursor: pointer;

  z-index: 5;
  transition: 0.3s;
}

.prev {
  left: 20px;
}

.next {
  right: 20px;
}

.prev:hover,
.next:hover {
  background: black;
  transform: translateY(-50%) scale(1.1);
}

/* Dots */

.dots {
  display: flex;
  gap: 10px;

  margin-top: 25px;
}

.dot {
  width: 14px;
  height: 14px;

  padding: 0;
  border: none;

  border-radius: 50%;

  background: #bbb;

  cursor: pointer;
  transition: 0.3s;
}

.dot.active {
  background: #222;
  transform: scale(1.3);
}

.carousel-container p {
  margin-top: 15px;

  color: #555;
  font-size: 18px;
}

/* Mobile */

@media (max-width: 600px) {
  .carousel-container h1 {
    font-size: 28px;
  }

  .carousel {
    height: 280px;
  }

  .prev,
  .next {
    width: 45px;
    height: 45px;

    font-size: 20px;
  }
}
```
index.css
```
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html,
body,
#root {
  width: 100%;
  min-height: 100%;
}
```
main.jsx
```
import React from "react";
import ReactDOM from "react-dom/client";

import App from "./App";
import "./index.css";

ReactDOM.createRoot(
  document.getElementById("root")
).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```
## OUTPUT
<img width="928" height="547" alt="Screenshot 2026-09-15 095527" src="https://github.com/user-attachments/assets/b041cb8a-89c5-4ac8-9cd7-bfe3c47243b3" />
<img width="1032" height="612" alt="Screenshot 2026-09-15 095430" src="https://github.com/user-attachments/assets/c6285e78-1c4d-486d-8daf-79f3d05adec8" />
<img width="1018" height="570" alt="Screenshot 2026-09-15 095445" src="https://github.com/user-attachments/assets/877802c0-084e-43eb-9589-07fe22860a3e" />
<img width="1035" height="587" alt="Screenshot 2026-09-15 095457" src="https://github.com/user-attachments/assets/4c32e6b6-778e-434f-9866-eab160c45b18" />






## RESULT
The program for creating Image Carousel using React is executed successfully.
