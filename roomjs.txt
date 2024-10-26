let slideImages = document.querySelectorAll('.slides img');
let next = document.querySelector('.next');
let prev = document.querySelector('.prev');
let dots = document.querySelectorAll('.dot');

let counter = 0;

next.addEventListener('click', slideNext);
prev.addEventListener('click', slidePrev);

function updateDots() {
    dots.forEach(dot => dot.classList.remove('active'));
    dots[counter].classList.add('active');
}

function slideNext() {
    slideImages[counter].classList.remove('active');
    slideImages[counter].style.animation = 'next1 0.5s ease-in forwards';
    counter = (counter + 1) % slideImages.length;
    slideImages[counter].classList.add('active');
    slideImages[counter].style.animation = 'next2 0.5s ease-in forwards';
    updateDots();
}

function slidePrev() {
    slideImages[counter].classList.remove('active');
    slideImages[counter].style.animation = 'prev1 0.5s ease-in forwards';
    counter = (counter - 1 + slideImages.length) % slideImages.length;
    slideImages[counter].classList.add('active');
    slideImages[counter].style.animation = 'prev2 0.5s ease-in forwards';
    updateDots();
}

dots.forEach(dot => {
    dot.addEventListener('click', () => {
        let index = parseInt(dot.getAttribute('attr'));
        slideImages[counter].classList.remove('active');
        if (index > counter) {
            slideImages[counter].style.animation = 'next1 0.5s ease-in forwards';
            slideImages[index].style.animation = 'next2 0.5s ease-in forwards';
        } else if (index < counter) {
            slideImages[counter].style.animation = 'prev1 0.5s ease-in forwards';
            slideImages[index].style.animation = 'prev2 0.5s ease-in forwards';
        }
        counter = index;
        slideImages[counter].classList.add('active');
        updateDots();
    });
});
