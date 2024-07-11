# FROM python:3.11.9
# WORKDIR /app
# COPY . /app

# ENV POETRY_VERSION=1.8.3 \
#     # make poetry install to this location
#     POETRY_HOME="/opt/poetry" \
#     # make poetry create the virtual environment in the project's root
#     # it gets named `.venv`
#     POETRY_VIRTUALENVS_IN_PROJECT=true \
#     # do not ask any interactive question
#     POETRY_NO_INTERACTION=1 

# ENV PATH="$POETRY_HOME/bin:$PATH"

# RUN curl -sSL https://install.python-poetry.org | python3 -

# COPY poetry.lock pyproject.toml /app/

# RUN poetry install 

# # RUN poetry run bash ./prestart.sh

# RUN pip install --no-cache-dir poetry && \
#     poetry config virtualenvs.create false && \
#     poetry install --no-dev

# EXPOSE 8000

# # CMD poetry run bash ./prestart.sh; poetry run uvicorn app.main:app --host 0.0.0.0 --port 8000
# CMD poetry run uvicorn app.main:app --reload



FROM python:3.10-slim
    
# Set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Set the working directory in the container
WORKDIR /app

# Install Poetry
RUN pip install poetry

# Copy only the dependency files to optimize caching
COPY poetry.lock pyproject.toml /app/

# Install dependencies
RUN poetry config virtualenvs.create false \
    && poetry install --no-dev --no-interaction --no-ansi

# Copy the application code into the container
COPY . /app/

# Expose the port where FastAPI runs (adjust if necessary)
EXPOSE 8000

CMD poetry run bash ./prestart.sh; poetry run uvicorn app.main:app --host 0.0.0.0 --port 8000
