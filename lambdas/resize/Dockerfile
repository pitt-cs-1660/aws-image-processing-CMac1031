FROM public.ecr.aws/lambda/python:3.13

# install uv
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

############
#
# TODO: implement the rest of the image
#
############
COPY pyproject.toml ${LAMBDA_TASK_ROOT}/

#rest of your enviroment variables
# build virtual environment and install dependencies
WORKDIR ${LAMBDA_TASK_ROOT}
COPY pyproject.toml ./

RUN uv venv .venv && \
    uv pip install -e .

# Copy your Lambda handler code
COPY . .
## set PYTHONPATH to include the virtual environment site-packages
ENV PYTHONPATH="${LAMBDA_TASK_ROOT}/.venv/lib/python3.13/site-packages"

# set the CMD to your handler
CMD [ "handler.resize_handler"]