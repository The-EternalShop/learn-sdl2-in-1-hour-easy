# Learn SDL2 in 1 Hour!

Wanna learn SDL2? You can learn it here!

## Step 1: Set Up Your Build Environment

Install SDL2 and, SDL_image if you're unlucky, and also use brew and the official installation for maximum compatibility, not like that will do anything bad (foreshadowing). Then copy and paste this code into a file called Makefile or else:

```Makefile
main: $(wildcard *.cpp)
	g++ $(wildcard *.cpp) -o main -F/Library/Frameworks -framework SDL2 -std=c++17 -Wl,-rpath,/Library/Frameworks
```

## Step 2: Make Sure You're Running This On A Mac

If you are running this on a non-Mac, then, umm, bad things will happen.(We not sayin what) Also try to replicate step 1 exactly, if you get my drift.

## Step 3: Copy the File

Should be the easiest step; this is just as comprehendable as, Spanish?

```cpp
#include <SDL2/SDL.h>
#include <iostream>

using namespace std;

int main(int argc, char* argv[]) {
    if (SDL_Init(SDL_INIT_VIDEO) < 0) {
        cerr << "Failed to initialize SDL: " << SDL_GetError() << endl;
        return -1;
    }

    SDL_Window* window = SDL_CreateWindow(
        "Lego Island 2D Clone",
        SDL_WINDOWPOS_CENTERED, SDL_WINDOWPOS_CENTERED,
        800, 600,
        SDL_WINDOW_SHOWN
    );

    if (!window) {
        cerr << "Failed to create window: " << SDL_GetError() << endl;
        SDL_Quit();
        return -1;
    }

    SDL_Renderer* renderer = SDL_CreateRenderer(window, -1, SDL_RENDERER_ACCELERATED);
    if (!renderer) {
        cerr << "Failed to create renderer: " << SDL_GetError() << endl;
        SDL_DestroyWindow(window);
        SDL_Quit();
        return -1;
    }

    bool running = true;
    SDL_Event event;
    while (running) {
        while (SDL_PollEvent(&event)) {
            if (event.type == SDL_QUIT) {
                running = false;
            }
        }

        SDL_SetRenderDrawColor(renderer, 255, 0, 0, 255);
        SDL_RenderClear(renderer);

        SDL_RenderPresent(renderer);

        SDL_Delay(16);
    }

    SDL_DestroyRenderer(renderer);
    SDL_DestroyWindow(window);
    SDL_Quit();
    return 0;
}
```

## Step 4: Run This Command

`make; ./main` If this fails, good luck! Ok bye for now! Yeah we don't care if your compter crashes because you ran it on a non-Mac
