<template>
    <div class="container-fluid px-sm-5 py-3 py-sm-0">
                    <div class="row g-5 my-sm-2">
                        <div class="col-md-12">
                            <div class="card p-sm-3 bg-secondary shadow-sm d-flex rounded" style="min-height: 78.5vh;">
                                <div class="container" style="margin-top: 1.4rem;">
                                    <div class="row">
                                        <div class="col-md-6">
                                            <div class="row mb-4">
                                                <div class="col-12">
                                                    <div class="mb-4" style="max-width: 82%;">
                                                        <label for="formFile" class="form-label mb-3 fs-5">Importar archivo</label>
                                                        <input class="form-control form-control-sm" type="file" id="formFile" accept=".rsa">
                                                    </div>
                                                </div>
                                                <div class="col-3 d-grid mb-3">
                                                    <button type="button" value="0" name="" id="btnLeer" class="btn btn-secondary p-1" disabled>
                                                        <span>Leer</span>
                                                    </button>
                                                </div>
                                                <div class="col-3 d-grid mb-3">
                                                    <button type="button" value="0" name="" id="btnEjecutar" class="btn btn-secondary p-1" disabled>
                                                        <span>Ejecutar</span>
                                                    </button>
                                                </div>
                                            </div>
                                            <div class="row mb-4">
                                                <div class="col-12">
                                                    <div class="mb-3" style="max-width: 82%;">
                                                        <span class="form-label mb-3 fs-5">Entrada ejecución 01</span>
                                                    </div>
                                                </div>
                                                <div class="col-3 d-grid mb-3">
                                                    <button type="button" value="0" name="" id="btnIniciar" class="btn btn-secondary p-1" disabled>
                                                        <span>Iniciar</span>
                                                    </button>
                                                </div>
                                                <div class="col-3 d-grid mb-3">
                                                    <button type="button" value="0" name="" id="btnParar" class="btn btn-secondary p-1" disabled>
                                                        <span>Parar</span>
                                                    </button>
                                                </div>
                                            </div>
                                        </div>
                                        <div class="col-md-6 float-end">
                                            <textarea class="form-control align-top mb-3" type="text" id="txtInfo" readonly style="height: 45vh; background-color:#ced4da; resize: none;"></textarea>
                                            <div class="row justify-content-end">
                                                <div class="col-auto mb-3">
                                                    <button type="button" value="0" name="" id="btnBloques" class="btn btn-secondary p-1" disabled>
                                                        <span>Abrir en bloques</span>
                                                    </button>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

</template>