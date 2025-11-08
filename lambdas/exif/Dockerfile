FROM public.ecr.aws/lambda/python:3.13

WORKDIR ${LAMBDA_TASK_ROOT}

# install uv
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

# copy project requirements file
COPY pyproject.toml ${LAMBDA_TASK_ROOT}/
RUN uv sync

# copy function code
COPY handler.py ${LAMBDA_TASK_ROOT}/


#  sync the project
RUN uv sync --locked --no-install-project --no-editable

## set PYTHONPATH to include the virtual environment site-packages
ENV PYTHONPATH="${LAMBDA_TASK_ROOT}/.venv/lib/python3.13/site-packages"

# set the CMD to your handler
CMD [ "handler.exif_handler"]