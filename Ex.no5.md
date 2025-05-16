# Ex05 Image Carousel

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
import Carousel from './Carousel.jsx';

const App = () => (
  <div className="p-4">
    <h1 className="text-2xl font-bold text-center mb-4">Image Carousel</h1>
    <Carousel />
  </div>
);

ReactDOM.render(<App />, document.getElementById('root'));
```

Carousel.jsx
```
const { useState, useEffect } = React;

const images = [
  'https://images.unsplash.com/photo-1507525428034-b723cf961d3e',
  'https://images.unsplash.com/photo-1519046904884-53103b34b206',
  'https://images.unsplash.com/photo-1476514525535-07fb3b4ae5f1',
  'https://images.unsplash.com/photo-1508739773434-c26b3d09e206'
];

const Carousel = () => {
  const [currentIndex, setCurrentIndex] = useState(0);

  const nextImage = () => {
    setCurrentIndex((prevIndex) => (prevIndex + 1) % images.length);
  };

  const prevImage = () => {
    setCurrentIndex((prevIndex) => (prevIndex - 1 + images.length) % images.length);
  };

  useEffect(() => {
    const interval = setInterval(nextImage, 3000);
    return () => clearInterval(interval);
  }, []);

  return (
    <div className="carousel-container">
      <img
        src={images[currentIndex]}
        alt={`Slide ${currentIndex + 1}`}
        className="carousel-image"
      />
      <button
        onClick={prevImage}
        className="carousel-button left"
      >
        ←
      </button>
      <button
        onClick={nextImage}
        className="carousel-button right"
      >
        →
      </button>
      <div className="carousel-indicators">
        {images.map((_, index) => (
          <div
            key={index}
            className={`indicator ${index === currentIndex ? 'active' : ''}`}
          ></div>
        ))}
      </div>
    </div>
  );
};

export default Carousel;
```


index.css
```
/* Tailwind CSS base styles */
@import 'https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css';

.min-h-screen {
  min-height: 100vh;
}

.bg-gray-100 {
  background-color: #f7fafc;
}

.flex {
  display: flex;
}

.items-center {
  align-items: center;
}

.justify-center {
  justify-content: center;
}

.p-4 {
  padding: 1rem;
}

.text-2xl {
  font-size: 1.5rem;
}

.font-bold {
  font-weight: 700;
}

.text-center {
  text-align: center;
}

.mb-4 {
  margin-bottom: 1rem;
}

/* Carousel-specific styles */
.carousel-container {
  position: relative;
  width: 100%;
  max-width: 32rem; /* max-w-2xl */
  margin-left: auto;
  margin-right: auto;
}

.carousel-image {
  width: 100%;
  height: 24rem; /* h-96 */
  object-fit: cover;
  border-radius: 0.5rem; /* rounded-lg */
}

.carousel-button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background-color: rgba(255, 255, 255, 0.5);
  padding: 0.5rem;
  border-radius: 9999px; /* rounded-full */
  transition: background-color 0.2s;
}

.carousel-button:hover {
  background-color: rgba(255, 255, 255, 0.75);
}

.carousel-button.left {
  left: 1rem; /* left-4 */
}

.carousel-button.right {
  right: 1rem; /* right-4 */
}

.carousel-indicators {
  position: absolute;
  bottom: 1rem; /* bottom-4 */
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 0.5rem; /* space-x-2 */
}

.indicator {
  width: 0.75rem; /* w-3 */
  height: 0.75rem; /* h-3 */
  border-radius: 9999px; /* rounded-full */
  background-color: #a0aec0; /* bg-gray-400 */
}

.indicator.active {
  background-color: #ffffff; /* bg-white */
}
```


## OUTPUT

![image](https://github.com/user-attachments/assets/4e771caf-fd48-4ee5-8ce3-42690a0e2534)


## RESULT
The program for creating Image Carousel using React is executed successfully.
