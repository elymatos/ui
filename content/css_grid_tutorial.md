# CSS Grid Complete Tutorial

## Table of Contents
1. [Introduction](#introduction)
2. [Basic Concepts](#basic-concepts)
3. [Grid Container Properties](#grid-container-properties)
4. [Grid Item Properties](#grid-item-properties)
5. [Practical Examples](#practical-examples)
6. [Advanced Techniques](#advanced-techniques)
7. [Best Practices](#best-practices)

## Introduction

CSS Grid Layout is a powerful two-dimensional layout system that allows you to create complex layouts with ease. Unlike Flexbox (which is one-dimensional), Grid can handle both rows and columns simultaneously, making it perfect for creating page layouts, card grids, and complex UI components.

## Basic Concepts

### Grid Container and Grid Items

```css
.grid-container {
  display: grid; /* Creates a grid container */
}

.grid-item {
  /* Grid items are direct children of the grid container */
}
```

### Grid Lines, Tracks, and Cells

- **Grid Lines**: The dividing lines that make up the structure of the grid
- **Grid Tracks**: The space between two grid lines (rows or columns)
- **Grid Cells**: The intersection of a row and column
- **Grid Areas**: Rectangular areas made up of one or more grid cells

## Grid Container Properties

### 1. Creating Columns and Rows

```css
.grid-container {
  display: grid;
  
  /* Define columns */
  grid-template-columns: 200px 1fr 100px; /* 3 columns: fixed, flexible, fixed */
  grid-template-columns: repeat(3, 1fr); /* 3 equal columns */
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); /* Responsive columns */
  
  /* Define rows */
  grid-template-rows: 100px auto 50px; /* 3 rows with different heights */
  grid-template-rows: repeat(3, 150px); /* 3 rows of 150px each */
}
```

### 2. Grid Gap

```css
.grid-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  
  /* Gap between grid items */
  gap: 20px; /* Same gap for rows and columns */
  gap: 20px 30px; /* Different gap: rows columns */
  
  /* Individual gaps */
  row-gap: 20px;
  column-gap: 30px;
}
```

### 3. Grid Template Areas

```css
.grid-container {
  display: grid;
  grid-template-columns: 1fr 3fr 1fr;
  grid-template-rows: auto 1fr auto;
  grid-template-areas: 
    "header header header"
    "sidebar main ads"
    "footer footer footer";
}

.header { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main { grid-area: main; }
.ads { grid-area: ads; }
.footer { grid-area: footer; }
```

### 4. Implicit Grid

```css
.grid-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  
  /* Control implicit rows/columns */
  grid-auto-rows: 150px; /* Height of auto-generated rows */
  grid-auto-columns: 200px; /* Width of auto-generated columns */
  grid-auto-flow: row; /* or column, row dense, column dense */
}
```

## Grid Item Properties

### 1. Grid Line Positioning

```css
.grid-item {
  /* Position by line numbers */
  grid-column-start: 2;
  grid-column-end: 4;
  grid-row-start: 1;
  grid-row-end: 3;
  
  /* Shorthand */
  grid-column: 2 / 4; /* start / end */
  grid-row: 1 / 3;
  
  /* Span syntax */
  grid-column: span 2; /* Span 2 columns */
  grid-row: span 3; /* Span 3 rows */
}
```

### 2. Grid Area

```css
.grid-item {
  /* Using named areas */
  grid-area: header;
  
  /* Using line numbers: row-start / column-start / row-end / column-end */
  grid-area: 1 / 2 / 3 / 4;
}
```

### 3. Alignment

```css
.grid-item {
  /* Align individual item */
  justify-self: center; /* horizontal alignment */
  align-self: center; /* vertical alignment */
  place-self: center; /* shorthand for both */
}

.grid-container {
  /* Align all items */
  justify-items: center; /* horizontal alignment for all items */
  align-items: center; /* vertical alignment for all items */
  place-items: center; /* shorthand for both */
  
  /* Align the entire grid */
  justify-content: center; /* horizontal alignment of grid */
  align-content: center; /* vertical alignment of grid */
  place-content: center; /* shorthand for both */
}
```

## Practical Examples

### Example 1: Basic Photo Gallery

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Photo Gallery</title>
    <style>
        .gallery {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            padding: 20px;
        }
        
        .photo {
            aspect-ratio: 1;
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4);
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 1.2rem;
            font-weight: bold;
        }
        
        .photo:nth-child(3n) {
            grid-column: span 2;
        }
    </style>
</head>
<body>
    <div class="gallery">
        <div class="photo">Photo 1</div>
        <div class="photo">Photo 2</div>
        <div class="photo">Photo 3</div>
        <div class="photo">Photo 4</div>
        <div class="photo">Photo 5</div>
        <div class="photo">Photo 6</div>
    </div>
</body>
</html>
```

### Example 2: Website Layout

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Website Layout</title>
    <style>
        body {
            margin: 0;
            font-family: Arial, sans-serif;
            height: 100vh;
        }
        
        .container {
            display: grid;
            grid-template-columns: 250px 1fr;
            grid-template-rows: 80px 1fr 60px;
            grid-template-areas: 
                "header header"
                "sidebar main"
                "footer footer";
            height: 100vh;
            gap: 1px;
            background: #ddd;
        }
        
        .header {
            grid-area: header;
            background: #333;
            color: white;
            display: flex;
            align-items: center;
            padding: 0 20px;
        }
        
        .sidebar {
            grid-area: sidebar;
            background: #f4f4f4;
            padding: 20px;
        }
        
        .main {
            grid-area: main;
            background: white;
            padding: 20px;
            overflow-y: auto;
        }
        
        .footer {
            grid-area: footer;
            background: #333;
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .nav-item {
            padding: 10px 0;
            border-bottom: 1px solid #ddd;
        }
        
        @media (max-width: 768px) {
            .container {
                grid-template-columns: 1fr;
                grid-template-rows: 80px auto 1fr 60px;
                grid-template-areas: 
                    "header"
                    "sidebar"
                    "main"
                    "footer";
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header class="header">
            <h1>My Website</h1>
        </header>
        
        <nav class="sidebar">
            <div class="nav-item">Home</div>
            <div class="nav-item">About</div>
            <div class="nav-item">Services</div>
            <div class="nav-item">Contact</div>
        </nav>
        
        <main class="main">
            <h2>Welcome to My Website</h2>
            <p>This is the main content area. It uses CSS Grid to create a responsive layout that adapts to different screen sizes.</p>
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
        </main>
        
        <footer class="footer">
            <p>&copy; 2024 My Website. All rights reserved.</p>
        </footer>
    </div>
</body>
</html>
```

### Example 3: Card Grid Layout

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Card Grid</title>
    <style>
        .card-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 20px;
            padding: 20px;
        }
        
        .card {
            background: white;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            overflow: hidden;
            transition: transform 0.3s ease;
        }
        
        .card:hover {
            transform: translateY(-5px);
        }
        
        .card-header {
            height: 200px;
            background: linear-gradient(45deg, #667eea, #764ba2);
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 1.5rem;
            font-weight: bold;
        }
        
        .card-body {
            padding: 20px;
        }
        
        .card-title {
            margin: 0 0 10px 0;
            font-size: 1.25rem;
            color: #333;
        }
        
        .card-text {
            color: #666;
            line-height: 1.6;
        }
        
        /* Featured card spans 2 columns */
        .card.featured {
            grid-column: span 2;
        }
        
        .card.featured .card-header {
            height: 250px;
            background: linear-gradient(45deg, #ff6b6b, #ee5a24);
        }
        
        @media (max-width: 768px) {
            .card.featured {
                grid-column: span 1;
            }
        }
    </style>
</head>
<body>
    <div class="card-grid">
        <div class="card featured">
            <div class="card-header">Featured</div>
            <div class="card-body">
                <h3 class="card-title">Featured Article</h3>
                <p class="card-text">This is a featured card that spans two columns on larger screens. It demonstrates how you can make certain grid items take up more space.</p>
            </div>
        </div>
        
        <div class="card">
            <div class="card-header">Card 1</div>
            <div class="card-body">
                <h3 class="card-title">Regular Card</h3>
                <p class="card-text">This is a regular card with standard content. Grid automatically places it in the available space.</p>
            </div>
        </div>
        
        <div class="card">
            <div class="card-header">Card 2</div>
            <div class="card-body">
                <h3 class="card-title">Another Card</h3>
                <p class="card-text">CSS Grid makes it easy to create responsive card layouts that adapt to different screen sizes.</p>
            </div>
        </div>
        
        <div class="card">
            <div class="card-header">Card 3</div>
            <div class="card-body">
                <h3 class="card-title">More Content</h3>
                <p class="card-text">Each card can contain different amounts of content, and Grid handles the layout automatically.</p>
            </div>
        </div>
    </div>
</body>
</html>
```

### Example 4: Dashboard Layout

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dashboard</title>
    <style>
        body {
            margin: 0;
            font-family: Arial, sans-serif;
            background: #f5f5f5;
        }
        
        .dashboard {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            grid-template-rows: auto auto auto auto;
            gap: 20px;
            padding: 20px;
            height: 100vh;
            box-sizing: border-box;
        }
        
        .widget {
            background: white;
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            display: flex;
            flex-direction: column;
        }
        
        .widget h3 {
            margin: 0 0 15px 0;
            color: #333;
        }
        
        .widget-stat {
            font-size: 2rem;
            font-weight: bold;
            color: #2c3e50;
        }
        
        .widget-chart {
            background: linear-gradient(45deg, #3498db, #2980b9);
            color: white;
            text-align: center;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
        }
        
        /* Widget positioning */
        .revenue { grid-column: 1 / 3; }
        .users { grid-column: 3; }
        .orders { grid-column: 4; }
        .chart1 { grid-column: 1 / 3; grid-row: 2 / 4; }
        .chart2 { grid-column: 3 / 5; grid-row: 2; }
        .recent { grid-column: 3 / 5; grid-row: 3; }
        .activity { grid-column: 1 / 5; grid-row: 4; }
        
        @media (max-width: 768px) {
            .dashboard {
                grid-template-columns: 1fr;
                grid-template-rows: repeat(7, auto);
            }
            
            .revenue,
            .users,
            .orders,
            .chart1,
            .chart2,
            .recent,
            .activity {
                grid-column: 1;
                grid-row: auto;
            }
        }
    </style>
</head>
<body>
    <div class="dashboard">
        <div class="widget revenue">
            <h3>Total Revenue</h3>
            <div class="widget-stat">$45,678</div>
            <p>↗ 12% from last month</p>
        </div>
        
        <div class="widget users">
            <h3>Active Users</h3>
            <div class="widget-stat">1,234</div>
            <p>↗ 5% from last week</p>
        </div>
        
        <div class="widget orders">
            <h3>Orders</h3>
            <div class="widget-stat">567</div>
            <p>↘ 3% from yesterday</p>
        </div>
        
        <div class="widget widget-chart chart1">
            <h3>Revenue Chart</h3>
            <p>Monthly revenue trends would go here</p>
        </div>
        
        <div class="widget widget-chart chart2">
            <h3>User Growth</h3>
            <p>User growth chart</p>
        </div>
        
        <div class="widget recent">
            <h3>Recent Activity</h3>
            <ul>
                <li>New user registered</li>
                <li>Order #1234 completed</li>
                <li>Payment received</li>
            </ul>
        </div>
        
        <div class="widget activity">
            <h3>Activity Timeline</h3>
            <p>This widget spans the full width and shows recent system activity.</p>
        </div>
    </div>
</body>
</html>
```

## Advanced Techniques

### 1. Responsive Grids with `auto-fit` and `auto-fill`

```css
/* auto-fit: Columns collapse when empty */
.grid-auto-fit {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
}

/* auto-fill: Maintains empty columns */
.grid-auto-fill {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: 20px;
}
```

### 2. Dense Grid Packing

```css
.dense-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-flow: row dense; /* Fills gaps automatically */
    gap: 10px;
}
```

### 3. Subgrid (Limited Support)

```css
.parent-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
}

.child-grid {
    display: grid;
    grid-column: span 2;
    grid-template-columns: subgrid; /* Inherits parent's column structure */
}
```

### 4. CSS Grid with Custom Properties

```css
.dynamic-grid {
    display: grid;
    grid-template-columns: repeat(var(--columns, 3), 1fr);
    gap: var(--gap, 20px);
}

/* Change via JavaScript or media queries */
@media (max-width: 768px) {
    .dynamic-grid {
        --columns: 1;
        --gap: 10px;
    }
}
```

## Best Practices

### 1. Use Meaningful Names

```css
.grid-container {
    grid-template-areas: 
        "header header header"
        "nav main aside"
        "footer footer footer";
}

/* Better than using numbers */
.header { grid-area: header; }
.nav { grid-area: nav; }
.main { grid-area: main; }
```

### 2. Combine with Flexbox

```css
.grid-item {
    display: flex; /* Use flexbox inside grid items */
    flex-direction: column;
    justify-content: center;
    align-items: center;
}
```

### 3. Progressive Enhancement

```css
/* Fallback for older browsers */
.grid-container {
    display: flex;
    flex-wrap: wrap;
}

.grid-item {
    flex: 1 1 300px;
    margin: 10px;
}

/* Grid enhancement */
@supports (display: grid) {
    .grid-container {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
        gap: 20px;
    }
    
    .grid-item {
        margin: 0;
    }
}
```

### 4. Accessibility Considerations

```css
.grid-container {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
}

/* Maintain logical tab order */
@media (max-width: 768px) {
    .grid-container {
        grid-auto-flow: row;
    }
}
```

## Common Units and Functions

### Fractional Units (fr)
- `1fr` = 1 fraction of available space
- `2fr` = 2 fractions (twice as much space)

### Sizing Functions
- `minmax(min, max)` = Size between min and max values
- `fit-content(size)` = Size based on content up to max
- `min-content` = Minimum size based on content
- `max-content` = Maximum size based on content

### Repeat Function
- `repeat(count, size)` = Repeat a pattern
- `repeat(auto-fit, size)` = Fit as many as possible
- `repeat(auto-fill, size)` = Fill with empty columns

## Browser Support

CSS Grid is supported in all modern browsers:
- Chrome 57+
- Firefox 52+
- Safari 10.1+
- Edge 16+
- iOS Safari 10.3+
- Android Chrome 57+

For older browsers, provide fallbacks using Flexbox or floats.

## Summary

CSS Grid is a powerful layout system that excels at:
- Creating complex, responsive layouts
- Aligning items in two dimensions
- Building dashboard and card-based interfaces
- Implementing traditional website layouts
- Creating magazine-style layouts

The key to mastering CSS Grid is understanding the relationship between grid containers and grid items, and how properties like `grid-template-columns`, `grid-template-rows`, and `grid-area` work together to create sophisticated layouts with minimal code.

Practice with these examples and experiment with different combinations to build your CSS Grid skills!