FROM jupyter/pyspark-notebook:latest

ARG conda_env=vscode_pyspark
ARG py_ver=3.11

RUN mamba create --yes -p "${CONDA_DIR}/envs/${conda_env}" python=${py_ver} ipython ipykernel && \
    mamba clean --all -f -y

RUN "${CONDA_DIR}/envs/${conda_env}/bin/python" -m ipykernel install --user --name="${conda_env}" && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

RUN "${CONDA_DIR}/envs/${conda_env}/bin/pip" install pyspark pandas --no-cache-dir

RUN echo "conda activate ${conda_env}" >> "${HOME}/.bashrc"