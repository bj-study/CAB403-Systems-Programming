# CAB403 Study Guide | 2023 Semester 1

Timothy Chappell | Notes for CAB403 at the Queensland University of Technology

## How to use this guide
There are two ways to read the book:
1. Reading the PDF output:
    1. Navigate to [./book/pdf/output.pdf](./book/pdf/output.pdf)
    2. Open the PDF
2. Running the book via HTML (this provides the better experience)
    1. Install [NPM](https://docs.npmjs.com/cli/v7/configuring-npm/install)
    2. Install [serve](https://www.npmjs.com/package/serve)
    3. Navigate to the `book` directory and serve the files
    ```bash
    cd <project>/book
    serve
    ```
    4. Open up the corresponding URL in your browser e.g. http://localhost:3000 

## Building locally
1. Install [Cargo](https://doc.rust-lang.org/cargo/getting-started/installation.html) 
2. Install [mdbook](https://rust-lang.github.io/mdBook/guide/installation.html)
4. Serve the book
    - Via NPM
        1. Build the book
        ```bash
        mdbook build
        ```
        2. Serve the book
        ```bash
        cd <project>/book
        serve
        ```
    - Via mdBook
        1. Serve the book
        ```bash
        mdbook serve --open
        ```

## Disclaimer
Although these documents may provide a decent learning experience on their own it is highly advised that you use these in-part with the lectures notes and videos provided to you by your lecturer. This is mainly due to the fact that overtime these guides may become outdated as the units themselves get updated.

It is also important to remember that these guides are written by students and as part should always be taken with a grain of salt, always read further into topics you don't understand and always do your own research on topics. These guides are designed to give you a brief description on each topic giving you a nice overview of the unit and a solid exam time revision document.

A note for programming units, when it comes to programming the best way to learn is not by reading theory but by practising in a practical way. Follow along with the guides but customize the exercises to your liking and make an attempt to utilise the language being learnt in home projects of your own.

