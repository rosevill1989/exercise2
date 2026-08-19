    <?php

session_start();


if (!isset($_SESSION['tasks'])) {
    $_SESSION['tasks'] = [];
}


if ($_SERVER['REQUEST_METHOD'] === 'POST' && isset($_POST['action'])) {
    if ($_POST['action'] === 'add' && !empty(trim($_POST['task']))) {
        
        $newTask = htmlspecialchars(trim($_POST['task']));
        $_SESSION['tasks'][] = $newTask;
    } elseif ($_POST['action'] === 'clear') {
        $_SESSION['tasks'] = [];
    }
    
    header("Location: " . $_SERVER['PHP_SELF']);
    exit;
}


if (isset($_GET['delete'])) {
    $id = (int)$_GET['delete'];
    if (isset($_SESSION['tasks'][$id])) {
        unset($_SESSION['tasks'][$id]);
        
        $_SESSION['tasks'] = array_values($_SESSION['tasks']); 
    }
    header("Location: " . $_SERVER['PHP_SELF']);
    exit;
}
?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>1-Page PHP Task Manager</title>
    <!-- Importing a modern font for a cleaner dashboard look -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        /* CSS: Modern UI Dashboard Styling */
        :root {
            --primary: #6366F1;       /* Indigo */
            --primary-hover: #4F46E5;
            --danger: #F43F5E;        /* Rose */
            --danger-hover: #E11D48;
            --bg-gradient: linear-gradient(135deg, #EEF2F6 0%, #E0E7FF 100%);
            --surface: #FFFFFF;
            --text-main: #1E293B;
            --text-muted: #64748B;
            --border: #E2E8F0;
            --shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.05), 0 8px 10px -6px rgba(0, 0, 0, 0.01);
            --radius: 14px;
        }
        
        body {
            font-family: 'Inter', system-ui, sans-serif;
            background: var(--bg-gradient);
            color: var(--text-main);
            display: flex;
            justify-content: center;
            align-items: flex-start;
            min-height: 100vh;
            padding-top: 8vh;
            margin: 0;
            box-sizing: border-box;
        }

        .container {
            background: var(--surface);
            padding: 35px 30px;
            border-radius: var(--radius);
            box-shadow: var(--shadow);
            width: 100%;
            max-width: 420px;
            border: 1px solid rgba(255, 255, 255, 0.6);
            animation: slideUp 0.4s ease-out;
        }

        @keyframes slideUp {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        h1 {
            margin-top: 0;
            text-align: center;
            color: var(--text-main);
            font-weight: 700;
            font-size: 24px;
            letter-spacing: -0.5px;
            margin-bottom: 25px;
        }

        .input-group {
            display: flex;
            gap: 12px;
            margin-bottom: 25px;
        }

        input[type="text"] {
            flex: 1;
            padding: 12px 16px;
            border: 2px solid var(--border);
            border-radius: 10px;
            font-size: 15px;
            font-family: inherit;
            outline: none;
            transition: all 0.2s ease;
            background: #F8FAFC;
        }

        input[type="text"]:focus {
            border-color: var(--primary);
            background: var(--surface);
            box-shadow: 0 0 0 4px rgba(99, 102, 241, 0.1);
        }

        button {
            padding: 12px 20px;
            border: none;
            border-radius: 10px;
            background-color: var(--primary);
            color: white;
            font-size: 15px;
            font-weight: 500;
            font-family: inherit;
            cursor: pointer;
            transition: all 0.2s ease;
            box-shadow: 0 2px 4px rgba(99, 102, 241, 0.2);
        }

        button:hover {
            background-color: var(--primary-hover);
            transform: translateY(-1px);
            box-shadow: 0 4px 6px rgba(99, 102, 241, 0.3);
        }

        button:active {
            transform: translateY(0);
        }

        ul {
            list-style: none;
            padding: 0;
            margin: 0;
        }

        li {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 14px 16px;
            background: var(--surface);
            border: 1px solid var(--border);
            margin-bottom: 10px;
            border-radius: 10px;
            transition: all 0.2s ease;
            animation: fadeIn 0.3s ease-in-out;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: scale(0.98); }
            to { opacity: 1; transform: scale(1); }
        }

        li:hover {
            border-color: #CBD5E1;
            box-shadow: 0 2px 8px rgba(0,0,0,0.04);
            transform: scale(1.01);
        }

        .task-text {
            cursor: pointer;
            flex: 1;
            user-select: none;
            font-size: 15px;
            color: var(--text-main);
            position: relative;
            transition: color 0.2s;
            padding-right: 15px;
        }

        /* Toggled via JavaScript */
        .completed {
            text-decoration: line-through;
            color: var(--text-muted);
            text-decoration-thickness: 2px;
            text-decoration-color: var(--text-muted);
        }

        .delete-btn {
            color: var(--text-muted);
            text-decoration: none;
            font-size: 13px;
            font-weight: 500;
            padding: 6px 12px;
            border-radius: 6px;
            background: #F1F5F9;
            transition: all 0.2s ease;
        }

        .delete-btn:hover {
            background: #FFE4E6;
            color: var(--danger);
        }

        .clear-form {
            margin-top: 25px;
            text-align: center;
        }

        .clear-btn {
            background-color: transparent;
            color: var(--text-muted);
            width: 100%;
            border: 2px dashed var(--border);
            box-shadow: none;
        }

        .clear-btn:hover {
            background-color: #FFF1F2;
            border-color: var(--danger);
            color: var(--danger);
            box-shadow: none;
        }

        .empty-state {
            text-align: center;
            color: var(--text-muted);
            font-size: 15px;
            padding: 20px 0;
            background: #F8FAFC;
            border-radius: 10px;
            border: 1px dashed var(--border);
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>My Tasks</h1>
        
        <!-- HTML: Form for PHP submission -->
        <form method="POST" class="input-group">
            <input type="hidden" name="action" value="add">
            <input type="text" name="task" id="taskInput" placeholder="What needs to be done?" required autocomplete="off">
            <button type="submit">Add</button>
        </form>

        <!-- HTML/PHP: Rendering the tasks list -->
        <ul id="taskList">
            <?php if (empty($_SESSION['tasks'])): ?>
                <p class="empty-state">No tasks yet. Add one above!</p>
            <?php else: ?>
                <?php foreach($_SESSION['tasks'] as $index => $task): ?>
                    <li>
                        <!-- The onclick triggers JavaScript function -->
                        <span class="task-text" onclick="toggleTask(this)"><?= $task ?></span>
                        <a href="?delete=<?= $index ?>" class="delete-btn" onclick="return confirmDelete()">Delete</a>
                    </li>
                <?php endforeach; ?>
            <?php endif; ?>
        </ul>

        <?php if (!empty($_SESSION['tasks'])): ?>
            <form method="POST" class="clear-form">
                <input type="hidden" name="action" value="clear">
                <button type="submit" class="clear-btn" onclick="return confirm('Are you sure you want to clear all tasks?')">Clear All Tasks</button>
            </form>
        <?php endif; ?>
    </div>

    <!-- JavaScript: Client-side interactions -->
    <script>
        // Auto-focus the input field when the page loads
        document.getElementById('taskInput').focus();

        // Toggle a 'completed' CSS class when clicking a task text
        function toggleTask(element) {
            element.classList.toggle('completed');
        }

        // Show a confirmation dialog before deleting a single task
        function confirmDelete() {
            return confirm('Delete this task?');
        }
    </script>
</body>
</html>c
