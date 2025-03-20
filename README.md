<div class="cool-div">
  <h1>Cool Div</h1>
  <p>This is a cool div that does something cool.</p>
</div>
.cool-div {
  position: relative;
  width: 200px;
  height: 200px;
  background-color: #f0f0f0;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  overflow: hidden;
  transition: transform 0.5s ease-in-out;
}

.cool-div:hover {
  transform: scale(1.1);
}

.cool-div h1 {
  position: absolute;
  top: 20px;
  left: 20px;
  font-size: 24px;
  color: #333;
  animation: fadeIn 1s ease-in-out;
}

.cool-div p {
  position: absolute;
  bottom: 20px;
  right: 20px;
  font-size: 16px;
  color: #666;
  animation: fadeIn 1s ease-in-out;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
