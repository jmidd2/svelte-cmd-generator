# Command Generator

This is a simple Svelte app that generates commands for the `rsync` program based on selected options. In the future
more programs will be added like `ssh`.

## Features

- Allows users to select options such as source and destination directories.
- Generates `rsync` commands based on the selected options.
- Provides the generated command for users to copy and use.

## Getting Started

### Prerequisites

Make sure you have Node.js and yarn installed on your machine.

### Installation

1. Clone this repository to your local machine:

   ```bash
   git clone https://github.com/jmidd2/svelte-cmd-generator.git
   ```

2. Navigate to the project directory:

   ```bash
   cd svelte-cmd-generator
   ```

3. Install dependencies:

   ```bash
   yarn install
   ```

### Running the App

To run the app locally, use the following command:

```bash
yarn run dev
```

The app will be accessible at `http://localhost:5173`.

### Usage

1. Select the source and destination directories.
2. Customize additional options such as excluding certain files or directories.
3. The generated `rsync` command will be displayed, ready for you to copy and use.
4. You can modify the options or extend the functionality as needed for your project.

### Deployment

To build the app for production, use the following command:

```bash
yarn run build
```

This will generate optimized files in the \`public\` directory, which you can deploy
