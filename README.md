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
</style># exercise2
